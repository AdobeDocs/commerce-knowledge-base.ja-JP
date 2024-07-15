---
title: 「MDVA-30186:GraphQL応答で属性オプションが並べ替えられていません」
description: MDVA-30186 パッチを適用すると、GraphQL レスポンスで属性オプションが並べ替えられない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.23 がインストールされている場合に利用できます。 パッチ ID は MDVA-30186。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 7b2aef16-5012-4206-9444-e0b765f0c0c9
feature: Attributes, GraphQL, Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# MDVA-30186:GraphQL応答で属性オプションが並べ替えられていません

MDVA-30186 パッチを適用すると、GraphQL レスポンスで属性オプションが並べ替えられない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.23 がインストールされている場合に使用できます。 パッチ ID は MDVA-30186。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.4 および 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 ～ 2.3.5-p2、2.4.0 ～ 2.4.0-p1、および 2.4.2 ～ 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. 既存のカラー属性に 3 つのオプションを追加します。
1. オプションを使用して 6 つのシンプルな製品を作成します（例：*オプション 1*:1 製品、*オプション 2*:2 製品、*オプション 3*:3 製品）。
1. カテゴリを作成し、上記で作成したすべての製品を割り当てます。
1. 次に、カテゴリ ID を使用して次のGraphQL リクエストを行います。

   <pre><code class="language-graphql">
    {
      products(
        filter: { category_id: { eq: "3" } }
        pageSize: 200
        currentPage: 1
        sort: { name: ASC }
      ) {
        aggregations {
          attribute_code
          count
          label
          options {
            count
            label
            value
          }
        }
        items {
          name
          sku
          url_key
        }
      }
    }
    </code></pre>

1. 次に、管理者の属性編集ページで属性オプションの並べ替え順を変更します。
1. 上記のGraphQL リクエストを再度行い、color 属性のオプションを確認します。

<u> 期待される結果 </u>:

属性オプションは、管理者が設定した順序に従って並べ替えられます。

<u> 実際の結果 </u>:

属性オプションは、常に関連する製品数に従って並べ替えられます。


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
