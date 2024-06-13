---
title: 非正規表現のオフロードにより、Nginx （ルート）ではなく Fastly にリダイレクトされる
description: このトピックでは、クラウドインフラストラクチャ上のAdobe Commerceで非正規表現リダイレクトを Nginx ではなく Fastly にオフロードする場合に発生する可能性がある、一般的なリダイレクトパフォーマンスの問題に対する解決策を示します。
exl-id: 8b22d25d-0865-4d21-b275-d344ba8748f2
feature: Routes
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# 非正規表現のオフロードにより、Nginx （ルート）ではなく Fastly にリダイレクトされる

このトピックでは、クラウドインフラストラクチャ上のAdobe Commerceで非正規表現リダイレクトを Nginx ではなく Fastly にオフロードする場合に発生する可能性がある、一般的なリダイレクトパフォーマンスの問題に対する解決策を示します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン） `Master/Production/Staging` fastly を活用した環境

## 問題

クラウドインフラストラクチャー上のAdobe Commerceでは、Nginx レイヤーで多数の非正規表現リダイレクト/書き換えを行うことができず、その結果、パフォーマンスの問題が発生する可能性があります。

## 原因：

この `routes.yaml` 内のファイル `.magento/routes.yaml` ディレクトリは、クラウドインフラストラクチャ上のAdobe Commerceのルートを定義します。

のサイズ `routes.yaml` ファイルが 32 KB 以上です。非正規表現のリダイレクト/書き換えを Fastly にオフロードする必要があります。

この Nginx レイヤーは、多数の非正規表現リダイレクト/書き換えを処理できません。処理しないと、パフォーマンスの問題が発生します。

## 解決策

解決策は、これらの非正規表現リダイレクトを Fastly にオフロードすることです。 Fastly にリダイレクトする汎用のエラーパスを作成します。

以下の手順では、Nginx ではなく Fastly にリダイレクトを設定する方法について詳しく説明します。

1. エッジ辞書を作成します。

   まず、を使用できます。 [Adobe Commerceの VCL スニペット](/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html) エッジディクショナリを定義する場合。 これはリダイレクトを含みます。

   いくつかの注意点を次に示します。

   * Fastly では、辞書のエントリに対して正規表現を行うことはできません。 完全に一致するだけです。 これらの制限について詳しくは、 [エッジ辞書の制限に関する Fastly のドキュメント](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries#limitations-and-considerations).
   * Fastly には、1 つの辞書に入力できるエントリは 1000 個までに制限されています。 Fastly はこの制限を拡大できますが、それは 3 番目の注意事項につながります。
   * エントリを更新し、更新された VCL をすべてのノードに配置するたびに、ディクショナリの拡張によりジオメトリのロード時間が長くなります。つまり、2000 エントリのディクショナリのロードは、1000 エントリのディクショナリのロードより 3 倍～4 倍遅くなります。 ただし、これは VCL をデプロイする（ディクショナリを更新する、または VCL 関数コードを変更する）場合にのみ問題になります。

     リクエストの処理に Fastly にかかる時間には影響しません。新しい設定のプッシュに Fastly にかかる時間に影響するだけです。

     一般的に、設定の変更には平均して数秒かかり、通常は 5～10 秒以内です。 したがって、ディクショナリ項目の 2 倍の増加は、設定がロールアウトされるまで 30 秒以上かかります。 4 倍の増加には 2 分近くかかります。 これにより、4 つ目の注意事項が追加されます。

   * エッジディクショナリへのエントリは 10,000 個というかなり厳しい制限があります。

   リダイレクトリストを整理することを強くお勧めします。 複数の辞書を使用できますが、VCL に対して行う更新は、Fastly 全体で実際に入力されるまでに数分かかることに注意してください。

1. URL を辞書と比較します。

   URL 検索が発生すると、一致するものが見つかった場合に、カスタムエラーコードを適用するように比較が行われます。

   別の VCL スニペットを使用して、次のようなものをに追加します。 `vcl_recv`:

   ```
        declare local var.redir-path STRING;
        set var.redir-path = table.lookup(redirects, std.tolower(req.url), "");
   
        if (var.redir-path != "") {
          error 912 var.redir-path;
        }
   ```

   ここでは、URL がテーブルエントリに存在するかどうかを確認しています。 その場合、内部 Fastly エラーを呼び出し、そのエラーにテーブルからのリダイレクト URL を渡します。

1. リダイレクトの管理。

   一致が見つかると、に定義されているアクションが実行されます `obj.status`、この場合は 301 永続的な移動リダイレクトになります。

   で最終的なスニペットを使用する `vcl_error` 301 エラーコードをクライアントに送り返すには、次の手順に従います。

   ```
     if (obj.status == 912) {
        set obj.http.location = obj.response;
        set obj.status = 301;
        set obj.response = "Moved Permanently";
        return(deliver);
          }
   ```

   このブロックを使用して、から渡されたエラーコードを確認しています `vcl_recv` が一致する場合は、渡されたエラーメッセージの場所を設定し、ステータスコードを 301 に、メッセージを「永続的に移動」に変更します。 この時点で、応答はクライアントに戻る準備ができているはずです。

### ステージサービス

>[!WARNING]
>
>これらの手順をすべて試す場合は、Adobe Commerce ステージング環境を設定することを強くお勧めします。 これにより、Fastly サービスに対してテストを実行し、すべてが期待どおりに動作することを確認できます。

Adobe Commerce ステージング環境を実行しないが、これらのリダイレクトの外観を確認したい場合は、Fastly で直接ステージアカウントを設定できます。

## 関連資料

* [Fastly VCL 参照](https://docs.fastly.com/vcl/)
* [ルートの設定](/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml.html) 開発者向けドキュメントを参照してください。
* [Fastly の設定](/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) 開発者向けドキュメントを参照してください。
* [VCL 正規表現チートシート](https://docs.fastly.com/en/guides/vcl-regular-expression-cheat-sheet) 開発者向けドキュメントを参照してください。
