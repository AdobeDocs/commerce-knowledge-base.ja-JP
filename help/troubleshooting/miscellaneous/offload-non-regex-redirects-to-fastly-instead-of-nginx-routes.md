---
title: '[!DNL regex]以外のオフロードは、[!DNL Nginx]ではなく[!DNL Fastly]にリダイレクトします（ルート）'
description: このトピックでは、Adobe Commerce on cloud infrastructureで[!DNL Nginx]ではなく[!DNL Fastly]に[!DNL regex]以外のリダイレクトをオフロードする際に発生する可能性がある、一般的なリダイレクトのパフォーマンスの問題に対する解決策について説明します。
exl-id: 8b22d25d-0865-4d21-b275-d344ba8748f2
feature: Routes
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%
---
# [!DNL regex]以外のオフロードは、[!DNL Nginx]ではなく[!DNL Fastly]にリダイレクトします（ルート）

このトピックでは、Adobe Commerce on cloud infrastructureで[!DNL Nginx]ではなく[!DNL Fastly]に[!DNL regex]以外のリダイレクトをオフロードする際に発生する可能性がある、一般的なリダイレクトのパフォーマンスの問題に対する解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure （すべてのバージョン） [!DNL Fastly]を活用している`Master/Production/Staging`環境

## イシュー

クラウド インフラストラクチャ上のAdobe Commerceでは、[!DNL Nginx] レイヤーで[!DNL regex]以外の多数のリダイレクト/書き換えを実行できず、パフォーマンスの問題が発生する可能性があります。

## 原因

`.magento/routes.yaml` ディレクトリの`routes.yaml` ファイルは、Adobe Commerce on cloud infrastructureのルートを定義します。

`routes.yaml` ファイルのサイズが32 KB以上の場合は、[!DNL regex]以外のリダイレクト/書き換えを[!DNL Fastly]にオフロードする必要があります。

この[!DNL Nginx] レイヤーでは、多数の[!DNL regex]以外のリダイレクト/書き換えを処理できないか、パフォーマンスの問題が発生します。

## Solution

解決策は、代わりに[!DNL regex]以外のリダイレクトを[!DNL Fastly]にオフロードすることです。 [!DNL Fastly]にリダイレクトする汎用エラーパスを作成します。

次の手順では、[!DNL Nginx]ではなく[!DNL Fastly]にリダイレクトを配置する方法について詳しく説明します。

1. Edge辞書の作成。

   まず、Adobe Commerce[&#128279;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html?lang=ja)で[!DNL VCL]  スニペットを使用して、エッジディクショナリを定義できます。 これにはリダイレクトが含まれます。

   これに対する注意事項：

   * [!DNL Fastly]は、辞書エントリに対して[!DNL regex]を実行できません。 完全一致です。 これらの制限について詳しくは、[[!DNL Fastly]のEdge ディクショナリの制限事項](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries#limitations-and-considerations)に関するドキュメントを参照してください。
   * [!DNL Fastly]は、1つの辞書に対して1000個のエントリの制限があります。 [!DNL Fastly]はこの制限を延長できますが、これは3つ目の注意事項につながります。
   * エントリを更新し、すべてのノードに[!DNL VCL]を更新してデプロイすると、ディクショナリを拡張すると、幾何学的な読み込み時間が増加します。つまり、2000 エントリのディクショナリは、実際には1000 エントリのディクショナリよりも3x～4倍遅く読み込まれます。 ただし、[!DNL VCL]をデプロイする場合（ディクショナリを更新するか、[!DNL VCL]関数コードを変更する場合）は、問題が発生するだけです。

     リクエストの処理にかかる時間には影響しません。[!DNL Fastly]が新しい設定をプッシュするのにかかる時間にのみ影響します。[!DNL Fastly]

     一般的に、設定の変更は平均で数秒かかり、通常5～10秒以下です。 したがって、辞書アイテムの2倍の増加は、設定をロールアウトするのに30秒以上かかります。 4倍の増加には2分近くかかります。 これは4つ目の注意点につながります。

   * エッジディクショナリには、10,000件のエントリという厳しい制限があります。

   リダイレクトリストを統合することを強くお勧めします。 複数の辞書を使用できますが、[!DNL VCL]に対して行った更新は、実際に[!DNL Fastly]全体に入力するのに数分かかることにご注意ください。

1. [!DNL URL]を辞書と比較します。

   [!DNL URL]参照が発生すると、一致が見つかった場合は、比較を行ってカスタムエラーコードを適用します。

   別の[!DNL VCL] スニペットを使用して、次のような内容を`vcl_recv`に追加します。

   ```
        declare local var.redir-path STRING;
        set var.redir-path = table.lookup(redirects, std.tolower(req.url), "");
   
        if (var.redir-path != "") {
          error 912 var.redir-path;
        }
   ```

   ここでは、テーブル エントリに[!DNL URL]が存在するかどうかを確認しています。 もしそうなら、内部[!DNL Fastly] エラーを呼び出し、そのエラーにテーブルからリダイレクト [!DNL URL]を渡します。

1. リダイレクトを管理します。

   一致が見つかった場合、その`obj.status`に対して定義されたアクションが実行されます。この場合、301の永続的な移動リダイレクトが実行されます。

   `vcl_error`の最後のスニペットを使用して、301 エラーコードをクライアントに送り返します。

   ```
     if (obj.status == 912) {
        set obj.http.location = obj.response;
        set obj.status = 301;
        set obj.response = "Moved Permanently";
        return(deliver);
          }
   ```

   このブロックでは、`vcl_recv`から渡されたエラーコードが一致するかどうかを確認します。一致する場合は、渡されたエラーメッセージに場所を設定し、ステータスコードを301に変更して、メッセージを「永続的に移動」に変更します。 その時点で、応答はクライアントに戻る準備ができているはずです。

### ステージサービス

>[!WARNING]
>
>これらの手順をすべて試す場合は、Adobe Commerce ステージング環境を設定することを強くお勧めします。 これにより、[!DNL Fastly] サービスに対してテストを実行して、すべてが期待どおりに動作することを確認できます。

Adobe Commerce ステージング環境を実行したくないが、これらのリダイレクトがどのように表示されるかを確認したい場合は、[!DNL Fastly]で直接ステージアカウントを設定できます。

## 関連トピックス

* [[!DNL Fastly VCL]参照](https://docs.fastly.com/vcl/)
* [開発者用ドキュメントのルートの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml.html?lang=ja)
* 開発者向けドキュメントの[&#x200B; セットアップ  [!DNL Fastly]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja)
* 開発者ドキュメントの[[!DNL VCL] 正規表現のチートシート &#x200B;](https://docs.fastly.com/en/guides/vcl-regular-expression-cheat-sheet)
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
