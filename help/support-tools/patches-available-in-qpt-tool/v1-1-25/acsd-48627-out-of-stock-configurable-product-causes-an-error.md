---
title: 「ACSD-48627：在庫切れの設定可能な商品がエラーの原因」
description: ACSD-48627 パッチを適用すると、在庫切れの設定可能な商品が、買い物かごの詳細を取得するGraphQL リクエストを送信する際にエラーを発生させるAdobe Commerceの問題を修正できます。
exl-id: e3048a91-1112-49a7-afcc-e6bb23208351
feature: Admin Workspace, Configuration, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# ACSD-48627：在庫切れの設定可能な商品がエラーの原因

ACSD-48627 パッチでは、在庫切れの設定可能な商品が、GraphQL リクエストを送信して買い物かごの詳細を取得する際にエラーを発生させる問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.25 がインストールされています。 パッチ ID は ACSD-48627 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

設定可能な商品の在庫切れが原因で、GraphQL リクエストを送信して買い物かごの詳細を取得する際にエラーが発生します。

<u>再現手順</u>:

1. 顧客アカウントを作成します。
1. 設定可能な製品を含め、いくつかの製品を買い物かごに追加します。
1. 管理バックエンドに移動し、すべての子製品数量を 0 に設定して設定可能な製品を編集します。
1. すべての子製品が在庫切れになったので、設定可能な製品は在庫切れになります。
1. を確認します `catalog_product_index_price` テーブル。 この商品のレコードは空です。
1. GraphQL リクエストを実行してカスタマートークンを取得します。

   ```GraphQL
   mutation {
       generateCustomerToken(
           email: "test@example.com"
           password: "xxxx"
           ) {
               token
               }
               }
   ```

1. GraphQL リクエストを実行して cartId を取得します。

   ```GraphQL
   Headers: Authentication => Bearer [customer token in step 6]
   ```

   ```GraphQL
   {
       customerCart {
           id
           items {
               id
               product {
                   name
                   sku
                   }
                   quantity
                   }
                   }
                   }
   ```

1. GraphQL リクエストを実行して、買い物かごの詳細を取得します。

   ```GraphQL
   Headers: Authentication => Bearer [customer token in step 6]
   ```

   ```GraphQL
   query GetCartDetails($cartId: String!) {
       cart(cart_id: $cartId) {
           id
           ...CartPageFragment
           __typename
           }
           }
           fragment CartPageFragment on Cart {
               id
               total_quantity
               ...AppliedCouponsFragment
               ...ProductListingFragment
               ...PriceSummaryFragment
               __typename
               }
               fragment AppliedCouponsFragment on Cart {
                   id
                   applied_coupons {
                       code
                       __typename
                       }
                       __typename
                       }
                       fragment ProductListingFragment on Cart {
                           id
                           items {
                               uid
                               product {
                                   uid
                                   name
                                   sku
                                   url_key
                                   url_suffix
                                   thumbnail {
                                       url
                                       __typename
                                       }
                                       small_image {
                                           url
                                           __typename
                                           }
                                           stock_status
                                           price_range {
                                               minimum_price {
   
                                               final_price {
                                                   currency
                                                   value
                                                   __typename
                                                   }
                                                   regular_price {
                                                       currency
                                                       value
                                                       __typename
                                                       }
                                                       __typename
                                                       }
                                                       __typename
                                                       }
                                                       stock_status
                                                       ... on ConfigurableProduct {
                                                           variants {
                                                               attributes {
                                                                   uid
                                                                   __typename
                                                                   }
                                                                   product {
                                                                       uid
                                                                       small_image {
                                                                           url
                                                                           __typename
                                                                           }
                                                                           stock_status
                                                                           __typename
                                                                           }
                                                                           __typename
                                                                           }
                                                                           __typename
                                                                           }
                                                                           __typename
                                                                           }
                                                                           prices {
                                                                               price {
                                                                                   currency
                                                                                   value
                                                                                   __typename
                                                                                   }
                                                                                   __typename
                                                                                   }
                                                                                   quantity
                                                                                   ... on
                                                                                   ConfigurableCartItem {
                                                                                       configurable_options {
                                                                                           id
                                                                                           configurable_product_option_uid
                                                                                           option_label
                                                                                           configurable_product_option_value_uid
                                                                                           value_label
                                                                                           __typename
                                                                                           }
                                                                                           __typename
                                                                                           }
                                                                                           __typename
                                                                                           }
                                                                                           __typename
                                                                                           }
                                                                                           fragment PriceSummaryFragment on Cart {
                                                                                               id
                                                                                               items {
                                                                                                   uid
                                                                                                   quantity
                                                                                                   __typename
                                                                                                   }
                                                                                                   ...ShippingSummaryFragment
                                                                                                   prices {
                                                                                                       ...TaxSummaryFragment
                                                                                                       ...DiscountSummaryFragment
                                                                                                       ...GrandTotalFragment
                                                                                                       subtotal_excluding_tax {
                                                                                                           currency
                                                                                                           value
                                                                                                           __typename
                                                                                                           }
                                                                                                           subtotal_including_tax {
                                                                                                               currency
                                                                                                               value
                                                                                                               __typename
                                                                                                               }
                                                                                                               __typename
                                                                                                               }
                                                                                                               __typename
                                                                                                               }
                                                                                                               fragment DiscountSummaryFragment on
                                                                                                               CartPrices {
                                                                                                                   discounts {
                                                                                                                       amount {
                                                                                                                           currency
                                                                                                                           value
                                                                                                                           __typename
                                                                                                                           }
                                                                                                                           label
                                                                                                                           __typename
                                                                                                                           }
                                                                                                                           __typename
                                                                                                                           }
                                                                                                                           fragment GrandTotalFragment on CartPrices {
                                                                                                                               grand_total {
                                                                                                                                   currency
                                                                                                                                   value
                                                                                                                                   __typename
                                                                                                                                   }
                                                                                                                                   __typename
                                                                                                                                   }
                                                                                                                                   fragment ShippingSummaryFragment on Cart {
                                                                                                                                       id
                                                                                                                                       shipping_addresses {
                                                                                                                                           selected_shipping_method {
                                                                                                                                               amount {
                                                                                                                                                   currency
                                                                                                                                                   value
                                                                                                                                                   __typename
                                                                                                                                                   }
                                                                                                                                                   __typename
                                                                                                                                                   }
                                                                                                                                                   street
                                                                                                                                                   __typename
                                                                                                                                                   }
                                                                                                                                                   __typename
                                                                                                                                                   }
                                                                                                                                                   fragment TaxSummaryFragment on CartPrices {
                                                                                                                                                       applied_taxes {
                                                                                                                                                           amount {
                                                                                                                                                               currency
                                                                                                                                                               value
                                                                                                                                                               __typename
                                                                                                                                                               }
                                                                                                                                                               __typename
                                                                                                                                                               }
                                                                                                                                                               __typename
                                                                                                                                                               }
   ```

<u>期待される結果</u>:

不可 *内部サーバーエラー* 応答で。

<u>実際の結果</u>:

次のものがあります *内部サーバーエラー* 応答で。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
