---
title: 「MDVA-42768：子商品の在庫切れ時にGraphQLが誤った価格を表示」
description: MDVA-42768 パッチは、設定可能な商品である子商品が在庫切れになっている場合に、GraphQLが誤った価格を表示する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-42768。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 012e7e21-e508-4449-98a6-4bdb41284c3a
feature: GraphQL, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# MDVA-42768：子商品の在庫切れ時にGraphQLで誤った価格が表示される

MDVA-42768 パッチは、設定可能な商品である子商品が在庫切れになっている場合に、GraphQLが誤った価格を表示する問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.10 がインストールされています。 パッチ ID は MDVA-42768。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な商品の子商品が在庫切れで、「在庫切れの商品を表示」設定が有効になっている場合、GraphQL クエリには商品の通常の価格が次のように表示されます **0**.

<u>前提条件</u>:

サンプルデータがインストールされている。

<u>再現手順</u>:

1. に移動して、Commerce管理者で在庫切れの表示設定を有効にします。 **ストア** > **設定** > **カタログ** > **在庫**.
1. 設定可能な製品を作成し、シンプルな子製品を割り当てます。
1. バリアント（シンプル）製品の在庫を次のように設定します **在庫切れ**.
1. 再インデックス。
1. 以下のGraphQL クエリを実行します。

   ```GraphQL
   query {
     products(filter: { sku: { eq: "MH01" } }) {
       items {
         sku
         price_range {
           minimum_price {
             regular_price {
               value
               currency
             }
             final_price {
               value
               currency
             }
             discount {
               amount_off
               percent_off
             }
           }
           maximum_price {
             regular_price {
               value
               currency
             }
             final_price {
               value
               currency
             }
             discount {
               amount_off
               percent_off
             }
           }
         }
       }
     }
   }
   ```

1. 「応答」セクションを確認します `minimum_price` > `regular price`.

<u>期待される結果</u>:

それに応答して、最低通常価格が 0 と表示されない。

<u>実際の結果</u>:

それに応じた最低通常価格= 0 です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
