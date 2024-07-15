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

MDVA-36170 パッチを適用すると、GraphQL クエリの結果がキャッシュされない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MDVA-36170。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.6

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.1 ～ 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL クエリの結果がキャッシュされない問題を修正しました。

<u> 再現手順 </u>:

マーチャントは、GraphQL キャッシュのGETメソッドを使用していますが、キャッシュされたデータを取得していません。

<pre>https://magento_url/graphql?query={ products （filter: {category_id: {eq: "2"}}、pageSize: 2000、currentPage: 1、sort: {position: ASC}） {
項目 {
  sku
  id
  名前
  説明 {
    html
  }
  url_key
  仕様
  画像 {
    ラベル
    gallery_url
  }
  __typename
  quantity_in
  small_image {
    gallery_url
    ラベル
  }
  product_price_range {
    maximum_price {
      final_price {
        value
      }
    }
    minimum_price {
      final_price {
        value
      }
    }
  }
  ConfigurableProduct { について
    バリアント {
      属性 {
        コード
        ラベル
        value_index
      }
      製品 {
        sku
        quantity_in
      }
    }
   }
  }
}
}}</pre>

<u> 期待される結果 </u>:

データはキャッシュされます。

<u> 実際の結果 </u>:

データはキャッシュされません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
