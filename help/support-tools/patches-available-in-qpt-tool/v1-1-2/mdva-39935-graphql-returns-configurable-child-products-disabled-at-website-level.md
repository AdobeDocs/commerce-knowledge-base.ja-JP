---
title: 「MDVA-39935:GraphQLが web サイトレベルで無効になっている設定可能な子製品を返す」
description: MDVA-39935 Adobe Commerce パッチは、GraphQLが web サイトレベルで無効になっている設定可能な子製品を返す問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39935。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 45bd6bd9-3572-4477-a689-d6b952a3290a
feature: GraphQL, Configuration, Products
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# MDVA-39935:GraphQLが web サイトレベルで無効になっている設定可能な子製品を返す

MDVA-39935 Adobe Commerce パッチは、GraphQLが web サイトレベルで無効になっている設定可能な子製品を返す問題を修正しました。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.2 がインストールされています。 パッチ ID は MDVA-39935。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQLは、web サイトレベルで無効になった後も、設定可能な子製品を返します。

<u>再現手順</u>:

1. の下で「在庫切れ商品を表示」オプションを有効にする **ストア** > **設定** > **カタログ** > **在庫** > **在庫オプション** > **在庫切れ商品の表示** > **はい**.
1. 次のいずれかを選択 **設定可能な製品** が 2 つを超えています **シンプル製品**.
1. 無効 **シンプルな製品** を作成して、 **設定可能な製品**.
1. を取得する **設定可能な製品** GraphQLを使用したデータ。

<pre>
  <code class="language-graphql">
{
  products(filter: { sku: { eq: "cp1" } }) {
    items {
      __typename
      name
      sku
      ... on ConfigurableProduct {
        variants {
          product {
            __typename
            name
            sku
            color
            stock_status
          }
        }
      }
    }
  }
}
</code>
</pre>

<u>期待される結果</u>:

無効になった製品は、バリアント結果には表示されません。

<u>実際の結果</u>:

無効な製品データは、バリアント結果で取得されます。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

Adobe Commerce用の高品質パッチの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md).
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md).

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
