---
title: 「MDVA-38447:「個別に表示されない」設定可能な子商品がGraphQL応答で返され、MySQL クエリが遅い」
description: MDVA-38447 Adobe Commerce パッチでは、「Not visible individually （個別に表示されない）」設定可能な子商品がGraphQL レスポンスで返され、カテゴリフィルターを使用したGraphQL商品クエリで MySQL の処理に時間がかかる問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-38447。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 302e7458-d9ea-466a-a2ac-d86a8ee3eca3
feature: B2B, GraphQL, Categories, Configuration, Products, Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# MDVA-38447：設定可能な子商品がGraphQL応答で返され、MySQL クエリが遅い

MDVA-38447 Adobe Commerce パッチでは、「Not visible individually （個別に表示されない）」設定可能な子商品がGraphQL レスポンスで返され、カテゴリフィルターを使用したGraphQL商品クエリで MySQL の処理に時間がかかる問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.2 がインストールされている場合に使用できます。 パッチ ID は MDVA-38447。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「個別に表示されない」設定可能な子商品がGraphQL応答で返され、カテゴリフィルターを使用したGraphQL商品クエリの低速な MySQL クエリが返されます。

<u> 前提条件 </u>:

B2B モジュールをインストールする必要があります。

<u> 再現手順 </u>:

1. シンプルな製品を「**個別には表示されない** に設定して、設定可能な製品を作成します。
1. **full reindex** を実行します。
1. 次のような **GraphQL クエリ** 実行します。

<pre>getfilteredProducts （
  $filter: ProductAttributeFilterInput!
  $sort: ProductAttributeSortInput!
  $search：文字列
  $pageSize: Int!
  $currentPage: Int!
） &lbrace;
  products （
    フィルター：$filter
    並べ替え：$sort
    検索：$search
    pageSize: $pageSize
    currentPage: $currentPage
  ） &lbrace;
    total_count
    page_info &lbrace;
      total_pages
      current_page
      page_size
    &rbrace;
    項目 &lbrace;
      名前
      sku
    &rbrace;
  &rbrace;
&rbrace;</pre>

変数：

<pre>{"filter":{"user_group":{"eq":"}},"search":"config-100","sort":{},"pageSize":200,"currentPage":1}
</pre>

<u> 期待される結果 </u>:

表示が「個別に表示されない」に設定されている製品は、応答では返されません。

<u> 実際の結果 </u>:

表示が「個別に表示されない」に設定されている製品が、応答で返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

Adobe Commerce用の高品質パッチの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
