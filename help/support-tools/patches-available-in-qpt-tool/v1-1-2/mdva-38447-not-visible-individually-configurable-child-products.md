---
title: 「MDVA-38447:「個別に表示されない」設定可能な子商品がGraphQL応答で返され、MySQL クエリが遅い」
description: MDVA-38447 Adobe Commerce パッチでは、「Not visible individually （個別に表示されない）」設定可能な子商品がGraphQL レスポンスで返され、カテゴリフィルターを使用したGraphQL商品クエリで MySQL の処理に時間がかかる問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-38447。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 302e7458-d9ea-466a-a2ac-d86a8ee3eca3
feature: B2B, GraphQL, Categories, Configuration, Products, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# MDVA-38447：設定可能な子商品がGraphQL応答で返され、MySQL クエリが遅い

MDVA-38447 Adobe Commerce パッチでは、「Not visible individually （個別に表示されない）」設定可能な子商品がGraphQL レスポンスで返され、カテゴリフィルターを使用したGraphQL商品クエリで MySQL の処理に時間がかかる問題を修正しました。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.2 がインストールされています。 パッチ ID は MDVA-38447。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「個別に表示されない」設定可能な子商品がGraphQL応答で返され、カテゴリフィルターを使用したGraphQL商品クエリの低速な MySQL クエリが返されます。

<u>前提条件</u>:

B2B モジュールをインストールする必要があります。

<u>再現手順</u>:

1. シンプルな製品をに設定して設定可能な製品を作成 **個別に表示されない**.
1. を実行 **フル再インデックス**.
1. を実行 **GraphQL クエリ** いいね！

<pre>クエリ getFilteredProducts （$filter: ProductAttributeFilterInput!
  $sort: ProductAttributeSortInput!
  $search：文字列$pageSize：整数！
  $currentPage: Int!
） { products （filter: $filter sort: $sort search: $search pageSize: $pageSize currentPage: $currentPage） { total_count page_info { total_pages current_page page_size } items { name sku } } }</pre>

変数：

<pre>{"filter":{"user_group":{"eq":"}},"search":"config-100","sort":{},"pageSize":200,"currentPage":1}
</pre>

<u>期待される結果</u>:

表示が「個別に表示されない」に設定されている製品は、応答では返されません。

<u>実際の結果</u>:

表示が「個別に表示されない」に設定されている製品が、応答で返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

Adobe Commerce用の高品質パッチの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
