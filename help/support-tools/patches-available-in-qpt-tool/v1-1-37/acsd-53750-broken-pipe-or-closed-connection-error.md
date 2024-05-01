---
title: 'ACSD-53750: マルチスレッド catalog_product_price reindex の実行中に「パイプが破損しているか、接続が閉じています」エラーが発生する'
description: ACSD-53750 パッチを適用すると、マルチスレッド catalog_product_price reindex の実行中に*Broken pipe or closed connection* エラーが発生するAdobe Commerceの問題を修正できます。
feature: Products
role: Admin, Developer
exl-id: afb30384-74e7-4857-9aff-8e99f5abc309
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# ACSD-53750: *壊れたパイプまたは閉じた接続* マルチスレッド中のエラー `catalog_product_price` 再インデックス

ACSD-53750 パッチは、 *壊れたパイプまたは閉じた接続* マルチスレッド中にエラーが発生しました `catalog_product_price` 再インデックス。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.37 がインストールされています。 パッチ ID は ACSD-53750 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*壊れたパイプまたは閉じた接続* マルチスレッド中にエラーが発生しました `catalog_product_price` 再インデックス。

<u>再現手順</u>:

1. RabbitMq を設定します。
1. 添付されたを使用してサンプルデータを生成します `small.xml` ファイル。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Config]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]** > **[!UICONTROL Inventory Indexer Setting]** およびを設定 **[!UICONTROL Stock/Source reindex strategy]** = **[!UICONTROL Asynchronous]**.
1. これをサポートするインデックスのディメンションモードを設定します。 例： `catalog_product_price_website_and_customer_group` または `customer_group`.

   ```
   bin/magento indexer:set-dimensions-mode catalog_product_price customer_group
   ```

1. のインデクサーのリセットを実行 `catalog_product_price`.

   ```
   bin/magento indexer:reset catalog_product_price
   ```

1. 複数のスレッドを使用して、リセットインデクサーのインデクサーを実行します。

   ```
   MAGE_INDEXER_THREADS_COUNT=10 bin/magento indexer:reindex catalog_product_price
   ```

<u>期待される結果</u>:

エラーは発生しません。

<u>実際の結果</u>:

AMQP 接続が原因で次のエラーが発生します： *壊れたパイプまたは閉じた接続*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
