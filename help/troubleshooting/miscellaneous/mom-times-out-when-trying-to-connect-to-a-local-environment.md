---
title: Adobe CommerceのMagento Order Managementシステム（OMS）がタイムアウトしました
description: ここでは、Adobe CommerceのMagento Order Managementシステム（OMS）が、コールバックを試みたときに MOM がタイムアウトするため、ngrok を使用してローカルにインストールされたマイクロサービスを MOM に登録できない問題の解決策について説明します。
exl-id: 19149d8c-ea24-46fb-8815-9f637afe46ca
feature: System
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Adobe CommerceのMagento Order Managementシステム（OMS）がタイムアウトしました

ここでは、Adobe CommerceのMagento Order Managementシステム（OMS）が、コールバックを試みたときに MOM がタイムアウトするため、ngrok を使用してローカルにインストールされたマイクロサービスを MOM に登録できない問題の解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.3.1
* OMS
* ngrok

>[!WARNING]
>
>免責事項：Adobe Commerceは、トンネルを確立するための特定のツールを推奨または推奨しません。 上記は提案のみです。 詳しくは、[ngrok のドキュメント &#x200B;](https://ngrok.com/docs) を参照してください。

## 問題

<u> 再現手順 </u>

1. ローカル環境にAdobe Commerceをインストールします。
1. ngrok を設定して、ローカルサーバーを公開するトンネルを作成します。
1. [OMS への接続 &#x200B;](https://commerce-docs.github.io/oms-documentation-archive/integration/connector/setup-tutorial/) を試します。

<u> 期待される結果 </u>

接続が正常に確立されました。

<u> 実際の結果 </u>

ngrok URL にコールバックしようとすると、MCOM がタイムアウトするようです。

## 原因：

このタイムアウトの考えられる理由の 1 つは、サーバーが地理的に遠すぎること、および接続に時間がかかりすぎることです。

## 解決策

ngrok の起動時に、地域を指定するパラメータを追加します。 例えば、次のようになります。

```bash
./ngrok http 80 -region eu
```

デフォルトのリージョンは US です。 [&#x200B; 使用可能なすべての値 &#x200B;](https://ngrok.com/docs#config_region) を参照してください。
