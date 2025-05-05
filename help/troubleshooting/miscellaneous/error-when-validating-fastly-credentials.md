---
title: Fastly 資格情報の検証中にエラーが発生する
description: この記事では、Fastly 資格情報の検証時にユーザーがエラーを受け取る問題の解決策を提供します。
exl-id: 02104731-6666-47a6-abc6-215812f09915
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Fastly 資格情報の検証中にエラーが発生する

この記事では、Fastly 資格情報の検証時にユーザーがエラーを受け取る問題の解決策を提供します。

## 問題

Fastly 資格情報の検証時にエラーが発生します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）：すべてのバージョン
* 拡張機能またはテクノロジー（Fastly、New Relicなど）のバージョン Fastly

## 解決策

1. 正しい Fastly サービス ID と API トークンがあることを確認して、もう一度検証を試してください。 詳しい手順については、開発者向けドキュメントの [Fastly 資格情報のテスト ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#test-the-fastly-credentials) を参照してください。
1. 資格情報の検証に失敗した場合は、次の curl コマンドを実行して、サービスのステータスを確認します。

   ```curl
   curl -H "Fastly-Key: <API key>" https://api.fastly.com/service/<service ID>/version/active
   ```

1. 上記のコマンドで *{&quot;msg&quot;:&quot;Token $TOKEN expired at 2021-09-28T02:03:37Z&quot;}* のようなエラーが返された場合は、サポートチケットを送信して新しい API トークンをリクエストします。

   サポートチケットの送信方法については、サポートナレッジベースの [Adobe Commerce ヘルプセンターユーザーガイド/サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#support-tickets) を参照してください。

   >[!NOTE]
   >
   >セキュリティ上の理由から、現在のトークンを失効させて新しいトークンを生成する必要があるので、パスワードや有効/アクティブな API トークンをチケットで直接共有しないでください。

1. コマンドがエラーを返さない場合は、[!DNL Fastly] 拡張機能の最新バージョンを実行していることを確認してください。 1.2.203 より前の古いバージョンを使用している場合は、まず「**[!UICONTROL Save Config]**」をクリックしてから資格情報をテストする必要があります。

## 開発者向けドキュメントの関連する読み値：

* [Cloud for Adobe Commerce/Fastly/Fastly サービスアカウントと資格情報 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly#fastly-service-account-and-credentials)

* [Cloud for Adobe Commerce/Fastly の設定/Fastly 資格情報のテスト ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration#test-the-fastly-credentials)
