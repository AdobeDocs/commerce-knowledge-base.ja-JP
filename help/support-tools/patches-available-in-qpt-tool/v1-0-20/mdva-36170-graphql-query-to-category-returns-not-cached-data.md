---
title: 「MDVA-36170：カテゴリへのGraphQL クエリで、キャッシュされていないデータが返される」
description: MDVA-36170 パッチを適用すると、GraphQL クエリの結果がキャッシュされない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.20 がインストールされている場合に利用できます。 パッチ ID は MDVA-36170。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 6249b751-4b71-4833-ab86-ded615d648a8
feature: Cache, GraphQL, Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# MDVA-36170：カテゴリへのGraphQL クエリで、キャッシュされていないデータが返される

MDVA-36170 パッチを適用すると、GraphQL クエリの結果がキャッシュされない問題が修正されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.20 がインストールされています。 パッチ ID は MDVA-36170。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.6

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.1 ～ 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL クエリの結果がキャッシュされない問題を修正しました。

<u>再現手順</u>:

マーチャントは、GraphQL キャッシュのGETメソッドを使用していますが、キャッシュされたデータを取得していません。

<pre>https://magento_url/graphql?query={ products （filter: {category_id: {eq: "2"}}, pageSize: 2000, currentPage: 1, sort: {position: ASC}） { items { sku id name description { html } url_key specifications image { label gallery_url } __typename quantity_in small_image { gallery_url label } product_price_range { maximum_price { final_price { value } } } minimum_price { final_price { value } } } .. on ConfigurableProduct { variants{ code label label label label value value value value value value index index index}}{{ product sku_in } } } } } }</pre>

<u>期待される結果</u>:

データはキャッシュされます。

<u>実際の結果</u>:

データはキャッシュされません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
