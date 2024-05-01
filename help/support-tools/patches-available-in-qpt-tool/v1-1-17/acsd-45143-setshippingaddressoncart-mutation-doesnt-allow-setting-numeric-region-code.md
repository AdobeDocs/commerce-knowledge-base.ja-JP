---
title: 「ACSD-45143:setShippingAddressesOnCart ミューテーションで、数値の地域コードが「地域」として設定されていない」
description: ACSD-45143 パッチでは、setShippingAddressesOnCart ミューテーションで数値地域コードが「地域」として設定されない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45143 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 5867ea97-7d54-486e-b5d0-bfb87f24fb80
feature: Orders, Shipping/Delivery, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# ACSD-45143: setShippingAddressesOnCart ミューテーションで、数値地域コードが「地域」として設定されていない

ACSD-45143 パッチでは、setShippingAddressesOnCart ミューテーションで数値地域コードが「地域」として設定されない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.17 がインストールされています。 パッチ ID は ACSD-45143 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

setShippingAddressesOnCart ミューテーションでは、数値地域コードを「地域」に設定することはできません。

<u>再現手順</u>:

1. 以下のクエリを使用して、買い物かごを作成します。

   <pre>
    <code class="language-graphql">
    mutation {
      createEmptyCart
    }
    </code>
    </pre>

1. 配送先住所をカートに設定するリクエストを送信します。

   <pre>
    <code class="language-graphql">
    mutation ($cartId: String!) {
      setShippingAddressesOnCart(
        input: {
          cart_id: $cartId
          shipping_addresses: {
            address: {
              firstname: "Tomek"
              lastname: "Nowak"
              company: "Company Name"
              street: ["234 Rue de Rivoli"]
              region: "58"
              city: "Lille"
              postcode: "59800"
              country_code: "FR"
              telephone: "123-456-0000"
              save_in_address_book: false
            }
          }
        }
        ) {
          cart {
            shipping_addresses {
              firstname
              lastname
              company
              street
              city
              region {
                code
                label
              }
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
      </code>
      </pre>

   注意：この例では、国コードは「FR」、地域コードは「58」に設定されています。 によると `directory_country_region` Db テーブル、リージョン・コード 58 は「Nièvre」です。

1. 返される応答を確認します。

<u>期待される結果</u>:

Adobe Commerceでは、GraphQL リクエストに数値のリージョンコードを設定できます。

<u>実際の結果</u>:

リージョンコードは 47 に変更されます。

<pre>
<code class="language-graphql">
{
  "data": {
    "setShippingAddressesOnCart": {
      "cart": {
        "shipping_addresses": [
        {
          "firstname": "Tomek",
          "lastname": "Nowak",
          "company": "Company Name",
          "street": [
          "234 Rue de Rivoli"
          ],
          "city": "Lille",
          "region": {
            "code": "47",
            "label": "Lot-et-Garonne"
            },
            "postcode": "59800",
            "telephone": "123-456-0000",
            "country": {
              "code": "FR",
              "label": "FR"
            }
          }
        ]
      }
    }
  }
}
</code>
</pre>

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
