---
title: 「ACSD-47937：アプリケーションレベルのキャッシュが原因で価格の降下通知が送信されない」
description: ACSD-47937 パッチを適用すると、アプリケーションレベルのキャッシングが原因で価格の低下を知らせるメッセージが常に送信されるとは限らないAdobe Commerceの問題を修正できます。
exl-id: f39c9ef6-4689-427f-bd61-3a52dec88be2
feature: Admin Workspace, Cache, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# ACSD-47937：アプリケーションレベルのキャッシュが原因で価格低下通知が送信されない

ACSD-47937 パッチは、アプリケーションレベルのキャッシュが原因で価格の低下の通知が常に送信されるとは限らない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされています。 パッチ ID は ACSD-47937 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 および 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4、2.4.5、2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

お客様は、その後の製品価格変更に関する製品価格の案内メールを受け取っていません。

<u>再現手順</u>:

1. Enable （有効） **[!UICONTROL Product Alert]** 両方に対して *[!UICONTROL Price Changes]* および *[!UICONTROL Back in Stock]* 。対象： **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Product Alert]**.
1. Enable （有効） **[!UICONTROL Display Out of Stock Products]**.
1. 数量= 0 の単純製品（ABC）を作成します。
1. ストアフロントから顧客を作成し、上記の製品を購読して、値下げ用の製品アラートを取得します。
1. 顧客の製品アラートを開始します。

   ```PHP
   bin/magento queue:consumers:start product_alert
   ```

1. ABC 商品の価格をドロップします。
1. 商品アラート cron をトリガーします。

   ```PHP
   php n98-magerun2.phar sys:cron:run catalog_product_alert
   ```

1. ABC 商品の価格をもう一度下げてください。
1. 商品アラート cron をトリガーします。

   ```PHP
   php n98-magerun2.phar sys:cron:run catalog_product_alert
   ```

>[!NOTE]
>
>詳しくない場合は、 [!DNL n98] その後、ツールを実行できます `bin/magento cron:run command` いつものように監視する `cron_schedule` 確認するテーブル `catalog_product_alert` ジョブは成功ステータスを取得します。

<u>期待される結果</u>:

2 つ目の価格ドロップメールが送信されます。

<u>実際の結果</u>:

2 番目の価格降下メールは送信されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
