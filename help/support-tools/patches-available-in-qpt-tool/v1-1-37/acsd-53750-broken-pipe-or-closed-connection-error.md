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

# ACSD-53750:*パイプの破損または接続の閉* マルチスレッド `catalog_product_price` の再インデックス中にエラーが発生しました

ACSD-53750 パッチは、マルチスレッド `catalog_product_price` のインデックス再作成中に *パイプの破損または接続の切断* エラーが発生する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.37 がインストールされている場合に使用できます。 パッチ ID は ACSD-53750 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p2

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

*パイプの破損または接続が閉じています* マルチスレッド `catalog_product_price` の再インデックス中にエラーが発生しました。

<u> 再現手順 </u>:

1. RabbitMq を設定します。
1. 添付された `small.xml` ファイルを使用してサンプルデータを生成します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Config]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]**/**[!UICONTROL Inventory Indexer Setting]** に移動し、**[!UICONTROL Stock/Source reindex strategy]** = **[!UICONTROL Asynchronous]** を設定します。
1. これをサポートするインデックスのディメンションモードを設定します。 例：`catalog_product_price_website_and_customer_group` または `customer_group`。

   ```
   bin/magento indexer:set-dimensions-mode catalog_product_price customer_group
   ```

1. `catalog_product_price` のインデクサーのリセットを実行します。

   ```
   bin/magento indexer:reset catalog_product_price
   ```

1. 複数のスレッドを使用して、リセットインデクサーのインデクサーを実行します。

   ```
   MAGE_INDEXER_THREADS_COUNT=10 bin/magento indexer:reindex catalog_product_price
   ```

<u> 期待される結果 </u>:

エラーは発生しません。

<u> 実際の結果 </u>:

AMQP 接続が原因で次のエラーが発生しました：*パイプが破損しているか、接続が閉じられています*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
