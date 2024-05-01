---
title: 「MDVA-43862:GraphQL UpdateCartItems ミューテーションエラーにより、顧客が買い物かご項目を更新できない」
description: MDVA-43862 パッチは、GraphQL UpdateCartItems ミューテーションエラーが原因で、お客様が買い物かごの商品を更新できない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-43862。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 5f0a2970-34a8-4a25-baf8-15c007f97084
feature: GraphQL, Orders, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# MDVA-43862:GraphQLの UpdateCartItems ミューテーションエラーにより、お客様が買い物かごの商品を更新できない

MDVA-43862 パッチは、GraphQL UpdateCartItems ミューテーションエラーが原因で、お客様が買い物かごの商品を更新できない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.13 がインストールされています。 パッチ ID は MDVA-43862。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1、2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL UpdateCartItems ミューテーションエラーが発生したので、お客様は買い物かご項目を更新できません。

<u>再現手順</u>:

1. 1 つの単純（MH01-XL-Gray）を割り当てて、設定可能な製品（MH01）を作成します。
1. Commerce管理者に移動します **カタログ** > **製品** > **SKU** > **MH01** > **カスタマイズ可能なオプション**.
1. 製品にカスタムオプションを追加します。
   * オプションタイトル：Option1
   * オプションタイプ：フィールド
   * 必須：はい
   * 価格：10.00
   * 価格タイプ：固定
   * SKU: MHC1
   * 最大文字数：25
1. 以下のGraphQL クエリを実行して、買い物かご ID を生成します。

   ```GraphQL
   mutation {
     createEmptyCart
   }
   ```

1. 買い物かごの ID コードをメモします。
1. 以下のクエリを実行して、設定可能な製品を買い物かごに追加します。

   ```GraphQL
   mutation {
   addConfigurableProductsToCart(
   input: {
       cart_id: "<cart ID from above step>",
       cart_items: [{
       parent_sku: "MH01",
       data: {
           quantity: 1,
           sku: "MH01-XL-Gray"
           },
           customizable_options: {
               id: 1,
               value_string: "2"
               }
           }
       ]
   }
   )
   {
   cart {
     items {
       uid
       quantity
       product {
         name
         sku
       }
       ... on ConfigurableCartItem {
         configurable_options {
           option_label
         }
       }
     }
   }
   }
   }
   ```

1. 設定可能な項目が買い物かごに入力されていることがわかります。
1. 返された uid をメモします。
1. ここでも、以下のクエリを実行して、買い物かご項目を更新します。

   ```GraphQL
   mutation {
     updateCartItems(
       input: {
         cart_id: "<cart ID from previous step>",
         cart_items: [
           {
             cart_item_uid: "<uid from previous step>"
             quantity: 3,
             customizable_options:[{
                 id: 1,
                 value_string: "67"
             }]
           }
         ]
       }
     ){
       cart {
         items {
           uid
           product {
             name
           }
           quantity
         }
         prices {
           grand_total{
             value
             currency
           }
         }
       }
     }
   }
   ```

1. 応答を確認します。

<u>期待される結果</u>:

買い物かごは問題なく更新されます。

<u>実際の結果</u>:

次のエラーが発生します。

```GraphQL
{
  "errors": [
    {
      "message": "Could not update cart item: You need to choose options for your item.",
      "extensions": {
        "category": "graphql-input"
      },
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "updateCartItems"
      ]
    }
  ],
  "data": {
    "updateCartItems": null
  }
}
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
