---
title: 「ACSD-57846：価格が 0 のフィルターを使用したGraphQL商品の検索で、結果が返されない」
description: ACSD-57846 パッチを適用すると、価格をゼロからフィルタリングすると、リクエストの形式が正しくなくなり  [!DNL OpenSearch]  結果が返されないAdobe Commerceの問題を修正できます。
feature: GraphQL, Products
role: Admin, Developer
source-git-commit: 490c7449761ded6aef10a838f27e1ea7671c6cc8
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# ACSD-57846:GraphQL商品の検索結果が返されない価格ゼロのフィルターを使用した検索

ACSD-57846 パッチは、価格をゼロからフィルタリングすると、[!DNL OpenSearch] へのリクエストの形式が正しくなくなり、結果が返されない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-57846 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQLの商品検索で価格が 0 の商品をフィルタリングすると、[!DNL OpenSearch] へのリクエストの形式が正しくなくなり、結果が返されません。

<u> 再現手順 </u>:

1. 次の 2 つのシンプルな製品でカテゴリを作成します。
   * simple1 – 価格$0
   * シンプル 2 – 価格$10
1. フロントエンドで両方の製品が表示されていることを確認します。
1. `price:{from:"1"}` でリクエストを送信します。

   ```graphql
   query {
     products(
       pageSize: 50
       currentPage: 1,
       filter: {price:{from:"1"}}
     ) {
       totalResult: total_count
       productItems: items {
         sku
         urlKey: url_key
         price: price_range {
           fullPrice: minimum_price {
             finalPrice: final_price {
               currency
               value
             }
           }
         }
       }
     }
   }
   ```

1. これにより、商品 *simple2* が返されます。
1. 次に、`price:{from:"0"}` でリクエストを送信します。

   ```graphql
   query {
     products(
       pageSize: 50
       currentPage: 1,
       filter: {price:{from:"0"}}
     ) {
       totalResult: total_count
       productItems: items {
         sku
         urlKey: url_key
         price: price_range {
           fullPrice: minimum_price {
             finalPrice: final_price {
               currency
               value
             }
           }
         }
       }
     }
   }
   ```

<u> 期待される結果 </u>:

*simple1* と *simple2* の両方の製品が返されます。

<u> 実際の結果 </u>:

製品は返されません。

```json
{
    "data": {
        "products": {
            "totalResult": 0,
            "productItems": []
        }
    }
}
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
