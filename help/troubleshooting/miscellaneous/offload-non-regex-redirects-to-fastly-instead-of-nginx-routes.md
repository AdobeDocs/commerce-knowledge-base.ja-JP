---
title: 「[!DNL regex] 以外のリダイレクトを  [!DNL Nginx]  ではなく  [!DNL Fastly]  （routes）にオフロードする」
description: ここでは、[!DNL regex] 以外のリダイレクトをクラウドインフラストラクチャのAdobe Commerceではなく  [!DNL Fastly]  にオフロードする場合に発生する可能性がある、一般的なリダイレク  [!DNL Nginx]  パフォーマンスの問題の解決策について説明します。
exl-id: 8b22d25d-0865-4d21-b275-d344ba8748f2
feature: Routes
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# [!DNL regex] 以外のリダイレクトを [!DNL Nginx] ではなく [!DNL Fastly] にオフロードする（ルート）

ここでは、クラウドインフラストラクチャー上のAdobe Commerceで、[!DNL regex] 以外のリダイレクトを [!DNL Nginx] ではなく [!DNL Fastly] にオフロードする場合に発生する可能性のある、一般的なリダイレクトパフォーマンスの問題の解決策について説明します。

## 影響を受ける製品とバージョン

* [!DNL Fastly] を活用した環境のクラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン） `Master/Production/Staging`

## 問題

クラウドインフラストラクチャー上のAdobe Commerceでは、[!DNL regex] 以外による大量のリダイレクトや書き換えを [!DNL Nginx] レイヤーで行うことができず、その結果、パフォーマンスの問題が発生する可能性があります。

## 原因：

`.magento/routes.yaml` ディレクトリの `routes.yaml` ファイルは、クラウドインフラストラクチャ上のAdobe Commerceのルートを定義します。

`routes.yaml` ファイルのサイズが 32 KB 以上の場合、[!DNL regex] 以外のリダイレクトや書き換えを [!DNL Fastly] にオフロードする必要があります。

この [!DNL Nginx] レイヤーは、[!DNL regex] 以外のリダイレクトや書き換えの数が多いと処理できません。そうしないと、パフォーマンスの問題が発生します。

## 解決策

解決策は、[!DNL regex] 以外のリダイレクトを [!DNL Fastly] にオフロードすることです。 [!DNL Fastly] にリダイレクトする汎用のエラーパスを作成します。

以下の手順では、[!DNL Nginx] ではなく [!DNL Fastly] にリダイレクトを配置する方法について詳しく説明します。

1. Edge Dictionary を作成します。

   まず、Adobe Commerceの [[!DNL VCL]  スニペット &#x200B;](/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html) を使用して、エッジディクショナリを定義できます。 これはリダイレクトを含みます。

   いくつかの注意点を次に示します。

   * 辞書のエントリに対して [!DNL regex] を実行で [!DNL Fastly] ません。 完全に一致するだけです。 これらの制限について詳しくは、edge 辞書の制限に関する [[!DNL Fastly] のドキュメントを参照してください &#x200B;](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries#limitations-and-considerations)。
   * [!DNL Fastly] には、1 つの辞書に対するエントリが 1000 個までに制限されています。 この制限は拡大で [!DNL Fastly] ますが、3 つ目の注意点があります。
   * エントリを更新し、その更新を [!DNL VCL] のすべてのノードにデプロイするたびに、辞書の拡張に伴ってジオメトリの読み込み時間が長くなります。つまり、2000 エントリの辞書は実際には 1,000 エントリの辞書よりも 3 倍～4 倍遅く読み込まれます。 ただし、これは [!DNL VCL] をデプロイする（ディクショナリを更新する、または [!DNL VCL] 関数コードを変更する）場合にのみ問題となります。

     リクエストの処理に要する時間には影響 [!DNL Fastly] ません。新しい設定のプッシュに要する時間 [!DNL Fastly] 影響するだけです。

     一般的に、設定の変更には平均して数秒かかり、通常は 5～10 秒以内です。 したがって、ディクショナリ項目の 2 倍の増加は、設定がロールアウトされるまで 30 秒以上かかります。 4 倍の増加には 2 分近くかかります。 これにより、4 つ目の注意事項が追加されます。

   * エッジディクショナリへのエントリは 10,000 個というかなり厳しい制限があります。

   リダイレクトリストを整理することを強くお勧めします。 複数の辞書を使用できますが、[!DNL VCL] ージに対して行う更新は、[!DNL Fastly] ージ全体で実際に入力されるまでに数分かかることに注意してください。

1. [!DNL URL] を辞書と比較してください。

   [!DNL URL] 検索が発生すると、一致が見つかった場合は比較が行われ、カスタムエラーコードが適用されます。

   別の [!DNL VCL] スニペットを使用して、次のようなものを `vcl_recv` に追加します。

   ```
        declare local var.redir-path STRING;
        set var.redir-path = table.lookup(redirects, std.tolower(req.url), "");
   
        if (var.redir-path != "") {
          error 912 var.redir-path;
        }
   ```

   ここでは、[!DNL URL] がテーブルエントリに存在するかどうかを確認しています。 発生した場合は、内部 [!DNL Fastly] エラーを呼び出し、そのエラーにリダイレクト [!DNL URL] テーブルから渡されます。

1. リダイレクトの管理。

   一致が見つかった場合は、その `obj.status` に対して定義されているアクション（この場合は 301 永続的な移動リダイレクト）が実行されます。

   `vcl_error` で最終的なスニペットを使用して、301 エラーコードをクライアントに送り返します。

   ```
     if (obj.status == 912) {
        set obj.http.location = obj.response;
        set obj.status = 301;
        set obj.response = "Moved Permanently";
        return(deliver);
          }
   ```

   このブロックでは、`vcl_recv` から渡されたエラーコードが一致するかどうかを確認しています。一致する場合は、渡されたエラーメッセージの場所を設定し、ステータスコードを 301 に、メッセージを「永続的に移動」に変更します。 この時点で、応答はクライアントに戻る準備ができているはずです。

### ステージサービス

>[!WARNING]
>
>これらの手順をすべて試す場合は、Adobe Commerce ステージング環境を設定することを強くお勧めします。 これにより、[!DNL Fastly] サービスに対してテストを実行し、すべてが期待どおりに動作することを確認できます。

Adobe Commerce ステージング環境を実行しないが、これらのリダイレクトの外観を確認したい場合は、[!DNL Fastly] で直接ステージアカウントを設定できます。

## 関連資料

* [[!DNL Fastly VCL]  参照 &#x200B;](https://docs.fastly.com/vcl/)
* 開発者向けドキュメントの [&#x200B; ルートの設定 &#x200B;](/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml.html)
* アドビの開発者向けドキュメントの [&#x200B; 設定  [!DNL Fastly]](/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html)
* 開発者向けドキュメントの [[!DNL VCL]  正規表現チートシート &#x200B;](https://docs.fastly.com/en/guides/vcl-regular-expression-cheat-sheet)
* Commerce実装プレイブックの [&#x200B; データベーステーブルを変更する際のベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
