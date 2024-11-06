---
title: 「MDVA-39521:GraphQL経由で買い物かごに配送先住所を設定できない」
description: MDVA-39521 パッチを使用すると、GraphQLを介して電話番号が空の買い物かごに配送先住所を設定できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39521。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: b6bb4e83-ba65-4f15-82be-1252d9beb2fb
feature: GraphQL, Orders, Shipping/Delivery, Shopping Cart
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# MDVA-39521:GraphQL経由で買い物かごに配送先住所を設定できない

MDVA-39521 パッチを使用すると、GraphQLを介して電話番号が空の買い物かごに配送先住所を設定できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.2 がインストールされている場合に使用できます。 パッチ ID は MDVA-39521。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「電話番号を表示」がオプションとして設定されているにもかかわらず、GraphQLを使用して、空の電話番号を持つ買い物かごに配送先住所を設定できない。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. **ストア**/**設定**/**カスタマー**/**カスタマー設定**/**名前と住所のオプション** に移動し、「電話を表示」をオプションとして設定します。
1. GraphQL リクエスト経由で空の買い物かごを作成します。

   ```GraphQL
   mutation {
   createEmptyCart
   }
   ```

1. 商品を買い物かごに追加します。

   ```GraphQL
   mutation {
   addSimpleProductsToCart(
   input: {
     cart_id: "{ CART_ID }"
     cart_items: [
       {
         data: {
           quantity: 1
           sku: "24-MG04"
         }
       }
     ]
   }
   ) {
   cart {
     items {
       id
       product {
         sku
         stock_status
       }
       quantity
     }
   }
   }
   }
   ```

1. アドレスを追加：GRAPHQL変数。

   ```GraphQL
   {
     "cartId": "6Efw00UbjPoP5cvTFhsswDTjpxs0Xupt"
   }
   ```

   ```GraphQL
   mutation ($cartId: String!) {
     setShippingAddressesOnCart(input: {cart_id: $cartId, shipping_addresses:
     {address: {firstname: "John", lastname: "Doe", company: "Company Name",
     street: ["820 Burrard Street"], city: "Vancouver", region: "BC", postcode: "V6Z 2J1",
     country_code: "CA", telephone: "123-456-0000", save_in_address_book: false}}}) {
       cart {
         shipping_addresses {
           firstname
           lastname
           company
           street
           city
           postcode
           telephone
           country {
             code
             label
           }
         }
       }
     }
   }
   ```

   結果：

   ```GraphQL
     {
         "data": {
             "setShippingAddressesOnCart": {
                 "cart": {
                     "shipping_addresses": [
                         {
                             "firstname": "John",
                             "lastname": "Canada",
                             "company": "Company Name",
                             "street": [
                                 "820 Burrard Street"
                             ],
                             "city": "Vancouver",
                             "postcode": "V6Z 2J1",
                             "telephone": "123-456-0000",
                             "country": {
                                 "code": "CA",
                                 "label": "CA"
                             }
                         }
                     ]
                 }
             }
         }
     }
   ```

1. 電話番号が空のアドレスを追加します。

   ```GraphQL
   mutation ($cartId: String!) {
     setShippingAddressesOnCart(input: {cart_id: $cartId, shipping_addresses: {address: {firstname:
       "John", lastname: "Canada", company: "Company Name", street: ["820 Burrard Street"], city:
       "Vancouver", region: "BC", postcode: "V6Z 2J1", country_code: "CA", telephone: "123-456-0000",
       save_in_address_book: false}}}) {
       cart {
         shipping_addresses {
           firstname
           lastname
           company
           street
           city
           postcode
           telephone
           country {
             code
             label
           }
         }
       }
     }
   }
   ```

<u> 期待される結果 </u>:

```GraphQL
 {
    "data": {
        "setShippingAddressesOnCart": {
            "cart": {
                "shipping_addresses": [
                    {
                        "firstname": "John",
                        "lastname": "Doe",
                        "company": "Company Name",
                        "street": [
                            "820 Burrard Street"
                        ],
                        "city": "Vancouver",
                        "postcode": "V6Z 2J1",
                        "telephone": "",
                        "country": {
                            "code": "CA",
                            "label": "CA"
                        }
                    }
                ]
            }
        }
    }
 }
```

<u> 実際の結果 </u>:

```GraphQL
{
    "data": {
        "setShippingAddressesOnCart": {
            "cart": {
                "shipping_addresses": []
            }
        }
    }
}
```

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
