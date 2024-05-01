---
title: 「MDVA-42341:「categoryList」GraphQL クエリで結果がフィルタリングされない」
description: MDVA-42341 パッチでは、リクエストに Store ヘッダーが含まれている場合に「categoryList」GraphQL クエリが結果をフィルタリングしない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.8 がインストールされている場合に利用できます。 パッチ ID は MDVA-42341。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 34aeb30a-9491-4102-b33e-dcd857b6a1c2
feature: GraphQL, Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# MDVA-42341:&quot;categoryList&quot; GraphQL クエリで結果がフィルターされない

MDVA-42341 パッチでは、リクエストに Store ヘッダーが含まれている場合に「categoryList」GraphQL クエリが結果をフィルタリングしない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.8 がインストールされています。 パッチ ID は MDVA-42341。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

リクエストにストアヘッダーがある場合、「categoryList」GraphQL クエリで結果がフィルタリングされない。

<u>再現手順</u>:

1. 新しいルートカテゴリを作成して名前を付けます **root2**.
1. 2 つ目の Web サイト/ストア/ストアレビューを作成して割り当て **root2** 新しいストアに移動します。
1. 「デフォルトのルートカテゴリ = category1」の下に新しいカテゴリを作成します。
1. GraphQL リクエストを使用して、2 番目の web サイトのカテゴリリストを取得します（Header store = new を使用）。

<pre>
<code class="language-graphql">
{
  categoryList(filters: {name: {match: "category1"}}) {
    uid
    level
    name
    breadcrumbs {
      category_uid
      category_name
      category_level
      category_url_key
    }
  }
}
</code>
</pre>

<u>期待される結果</u>:

「新規」ストアヘッダーを使用しているため、デフォルトのルートカテゴリのカテゴリは、応答に表示されません。

<u>実際の結果</u>:

デフォルトのルートカテゴリのカテゴリは、結果で使用できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
