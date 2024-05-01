---
title: 'ACSD-53925：を含む CMS ブロックを保存できない [!UICONTROL Product Carousel]'
description: ACSD-53925 パッチを適用すると、「catalog_product_price」のディメンションモードが web サイトに設定されている場合、管理者が製品カルーセルで CMS ブロックを保存できないAdobe Commerceの問題を修正できます。
feature: CMS, Page Builder, Price Indexer, Products
role: Admin, Developer
exl-id: 6ef6d8ff-4ebb-4adb-9fb7-0d4a81a25f50
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# ACSD-53925：を使用して CMS ブロックを保存できない *[!UICONTROL Product Carousel]*

ACSD-53925 パッチは、管理者がで CMS ブロックを保存できない問題を修正します *[!UICONTROL Product Carousel]* 次のディメンション モードの場合： `catalog_product_price` は web サイトに設定されています。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.43 がインストールされています。 パッチ ID は ACSD-53925 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者はで CMS ブロックを保存できません *[!UICONTROL Product Carousel]* 次のディメンション モードの場合： `catalog_product_price` は web サイトに設定されています。

<u>再現手順</u>:

1. 次の 2 つのシンプルな製品を作成します。
   * simple1 - $10
   * シンプル 2 - 20 ドル
1. バンドル製品「」を作成&#x200B;*bundle1-dyn*&#39;簡単な製品 SKU に基づく 2 つのオプションがあります。
1. 製品価格インデクサーの分析コード モードを設定します：

   `bin/magento indexer:set-dimensions-mode catalog_product_price website`

1. に移動 **[!UICONTROL Content]** > **[!UICONTROL Blocks]**&#x200B;新しい CMS ブロックを作成します。
1. を使用したコンテンツの編集 [!DNL Page Builder]:
   * を追加 *[!UICONTROL Row]* 要素
   * を追加 *[!UICONTROL Products]* 要素
   * を選択 *[!UICONTROL Product Carousel]*
   * 製品 SKU を入力 –  *bundle1-dyn*
1. CMS ブロックを保存します。

<u>期待される結果</u>:

ユーザーがエラーなく製品カルーセルを追加できる。

<u>実際の結果</u>:

* UI にメッセージがスローされます。 *このコンテンツの生成中にエラーが発生しました*
* `var/log/exception.log` 次のエラーが含まれます。

  ```
  [2023-08-18T20:58:14.533374+00:00] report.CRITICAL: PDOException: SQLSTATE[42S02]: Base table or view not found: 1146 Table 'username_dev.catalog_product_index_price_ws0' doesn't exist in /test/lib/internal/Magento/Framework/DB/Statement/Pdo/Mysql.php:90
  ```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
