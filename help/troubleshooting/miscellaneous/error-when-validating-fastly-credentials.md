---
title: 資格情報の検証中にエラーが発生  [!DNL Fastly]  ました
description: この記事では、資格情報の検証時にユーザーがエラーを受け取る問題の解決策  [!DNL Fastly]  説明します。
exl-id: 02104731-6666-47a6-abc6-215812f09915
feature: Configuration
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL Fastly] 資格情報の検証中にエラーが発生しました

この記事では、資格情報の検証時に発生した *トークン期限切れ* エラーの解決方法 [!DNL Fastly] 説明します。

この記事で説明する手順は、セキュリティ上の理由から [!DNL Fastly] API トークンをローテーション（サイクル）する必要がある場合にも適用されます。 このような場合、新しい [!DNL Fastly] API トークンをリクエストするために、Adobe Commerce サポートチケットを送信する必要があります。

## 問題

* [!DNL Fastly] 資格情報の検証時にエラーが発生します。
* 例えば、誤ってサポートチケットで共有されたり、公開フォーラムに投稿されたりした場合、[!DNL Fastly] トークンが侵害された可能性があります。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）：すべてのバージョン
* 拡張機能またはテクノロジー（[!DNL Fastly]、[!DNL New Relic] など）のバージョン [!DNL Fastly]

## 解決策

1. 正しい [!DNL Fastly] サービス ID と API トークンがあることを確認して、もう一度検証してみてください。 詳しい手順については、開発者向けドキュメントの [&#x200B; 資格情報  [!DNL Fastly]  テスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration?lang=en#test-the-fastly-credentials) を参照してください。
1. 資格情報の検証に失敗した場合は、次の curl コマンドを実行して、サービスのステータスを確認します。

   ```curl
   curl -H "Fastly-Key: <API key>" https://api.fastly.com/service/<service ID>/version/active
   ```

1. 上記のコマンドで `{"msg":"Token $TOKEN expired at 2021-09-28T02:03:37Z"}` のようなエラーが返された場合は、サポートチケットを送信して新しい API トークンをリクエストします。 新しいトークンを受信したら、環境の設定を更新します。

   サポートチケットの送信方法については、サポートナレッジベースの [Adobe Commerce ヘルプセンターユーザーガイド/サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-tickets) を参照してください。

   >[!NOTE]
   >
   >セキュリティ上の理由から、現在のトークンを失効させて新しいトークンを生成する必要があるので、パスワードや有効/アクティブな API トークンをチケットで直接共有しないでください。
   >
   >Adobe Commerce サポートはトークンにアクセスできるので、チケットにこの情報を含める必要はありません。

1. コマンドがエラーを返さない場合は、[!DNL Fastly] 拡張機能の最新バージョンを実行していることを確認してください。 1.2.203 より前の古いバージョンを使用している場合は、まず「**[!UICONTROL Save Config]**」をクリックしてから資格情報をテストする必要があります。

## 開発者向けドキュメントの関連する読み値：

* [Cloud for Adobe Commerce > [!DNL Fastly] > [!DNL Fastly]  サービスアカウントと資格情報 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly?lang=en#fastly-service-account-and-credentials)

* [Cloud for Adobe Commerce/設定  [!DNL Fastly] /資格情報  [!DNL Fastly]  テスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration?lang=en#test-the-fastly-credentials)
