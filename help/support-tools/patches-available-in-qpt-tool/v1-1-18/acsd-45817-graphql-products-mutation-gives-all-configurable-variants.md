---
title: 「ACSD-45817:GraphQL製品ミューテーションにより、すべての設定可能なバリアントが提供される」
description: ACSD-45817 パッチは、特定のストアのGraphQL「products」ミューテーションが、リクエストされたストアに割り当てられていないものを含め、設定可能なすべてのバリアントを返す問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.18 がインストールされている場合に利用できます。 パッチ ID は ACSD-45817 です。 この問題はAdobe Commerce 2.4.4 で修正されました。
exl-id: 3d61d1aa-36b5-471d-929b-7df8ce65c791
feature: GraphQL, Configuration, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# ACSD-45817:GraphQL製品のミューテーションで、すべての設定可能なバリアントが提供されます

ACSD-45817 パッチは、特定のストアに対するGraphQL `products` のミューテーションが、リクエストされたストアに割り当てられていないものを含め、設定可能なすべてのバリアントを返す問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.18 がインストールされている場合に使用できます。 パッチ ID は ACSD-45817 です。 この問題はAdobe Commerce 2.4.4 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.3-p3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特定のストアに対するGraphQL `products` ミューテーションは、リクエストされたストアに割り当てられていないものを含め、設定可能なすべてのバリアントを返します。

<u> 前提条件 </u>:

2 番目の web サイト、2 番目のストア、2 番目のストア表示を作成します。

<u> 再現手順 </u>:

1. 「configurable-a」と「configurable-b」の 2 つのサブ製品を持つ設定可能な製品を作成します。
1. 設定可能な製品を両方の web サイトに割り当てます。
1. 2 つ目の web サイトに「設定可能な」 a バリエーションを 1 つだけ割り当てます。
1. **ストアフロント** に移動し、2 つ目の web サイトに切り替えて、設定可能な製品を開きます。
1. 「configurable-a」という子オプションが 1 つだけ表示されていることを確認します。
1. エンドポイントを使用してGraphQL クエリ `POST: /graphql` 実行し、次の操作を実 `Headers: "store" = "new"` します

   ```GraphQL
   {
     products(filter: { sku: { eq: "configurable" } }) {
       items {
         id
         attribute_set_id
         name
         sku
         __typename
         price_range{
           minimum_price{
             regular_price{
               value
               currency
             }
           }
         }
         categories {
           id
         }
         ... on ConfigurableProduct {
           configurable_options {
             id
             attribute_id_v2
             label
             position
             use_default
             attribute_code
             values {
               value_index
               label
             }
             product_id
           }
           variants {
             product {
               id
               name
               sku
               attribute_set_id
               ... on PhysicalProductInterface {
                 weight
               }
               price_range{
                 minimum_price{
                   regular_price{
                     value
                     currency
                   }
                 }
               }
             }
             attributes {
               uid
               label
               code
               value_index
             }
           }
         }
       }
     }
   }
   ```

<u> 期待される結果 </u>:

「configurable-b」バリエーションは 2 番目の web サイトに割り当てられていないので、応答には表示されません。

<u> 実際の結果 </u>:

「configurable-b」バリエーションが応答に表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
