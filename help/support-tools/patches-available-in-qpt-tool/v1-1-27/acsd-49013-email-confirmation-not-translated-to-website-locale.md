---
title: 「ACSD-49013：メールの確認が web サイトのロケールに翻訳されない」
description: ACSD-49013 パッチを適用すると、一括 API を使用して顧客を作成する際に、メールの確認が web サイトのロケールに翻訳されないAdobe Commerceの問題を修正できます。
exl-id: 68203bd4-021a-4736-a793-4b6663a9c66b
feature: Admin Workspace, Communications
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# ACSD-49013：メールの確認が web サイトのロケールに翻訳されない

ACSD-49013 パッチは、一括 API を使用して顧客を作成する際に、メールの確認が web サイトのロケールに翻訳されない問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-49013 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

一括 API を使用して顧客を作成する場合、メールの確認は web サイトのロケールに翻訳されません。

<u>再現手順</u>:

1. のような別のロケールをインストールします `de_DE`.
1. 設定 *RabbitMQ*.
1. 実行 `bin/magento setup:upgrade` でRabbitMQにキューをインストールし、言語パックを設定します。
1. に web サイトを追加作成します。 [!UICONTROL Admin] > **[!UICONTROL Stores]** > **[!UICONTROL All Stores]**.
1. この新しい Web サイトのロケールをに設定します `de_DE` 。対象： [!UICONTROL Admin] > **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL Locale Options]**.
1. API 呼び出しを実行して、一括 API を使用してカスタマーアカウントを作成します。 対応するを使用します `website_id`.

   `Endpoint: /rest/async/bulk/V1/customers`

   ```
   [{
       "customer": {
       "email": "test@example.com",
       "firstname": "test",
       "lastname": "test",
       "website_id": 2
       },
       "password": "Passw0rd!"
   }]
   ```

1. 実行 `bin/magento queue:consumers:start async.operations.all --single-thread --max-messages=10`.
1. 指定した Web サイトで顧客アカウントが正しく作成されていることがわかります。
1. 受信した電子メールで顧客登録を確認します。

<u>期待される結果</u>:

顧客は指定した web サイトで作成されるので、登録メールは、その web サイトのロケールを使用して送信されます。

<u>実際の結果</u>:

顧客は指定した web サイトで正しく作成されますが、登録メールは、一括 API が使用される場合、デフォルトのロケールを使用して送信されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
