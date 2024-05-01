---
title: 「ACSD-57394：の複数の並べ替え属性による製品の並べ替えが正しくありません [!DNL GraphQL]'
description: で複数の並べ替え属性を使用する場合に、商品が正しく並べ替えられないAdobe Commerceの問題を修正するために、ACSD-57394 パッチを適用してください [!DNL GraphQL].
feature: GraphQL, Products
role: Admin, Developer
exl-id: f2e24daa-43a0-46b2-80b2-4e0ee116b776
source-git-commit: 42712af2ce4337cd64b8dea555139e4252fb91cf
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# ACSD-57394：の複数の並べ替え属性による製品の間違った並べ替え [!DNL GraphQL]

ACSD-57394 パッチは、で複数の並べ替え属性を使用した場合に、製品が正しく並べ替えられない問題を修正しました [!DNL GraphQL]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.48 がインストールされています。 パッチ ID は ACSD-57394 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

で複数の並べ替え属性を使用すると、製品が正しく並べ替えられない [!DNL GraphQL].

<u>再現手順</u>:

1. 価格と名前が異なる製品をいくつか作成します。
1. カテゴリを作成し、作成した製品を割り当てます。
1. を送信 [!DNL GraphQL] 製品は、作成されたカテゴリのいくつかのクエリ *並べ替え* 属性。 例：

   ```
   {
   products(
     currentPage: 1
     pageSize: 10
     filter: {
       category_id: {
         eq :"3"
       }
     }
     sort: {  price: DESC, name: ASC, position: ASC
     }
   ){
   items{
     name
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
           }
      }
     }
    }
   ```

1. 作成後の応答の確認 *並べ替え* 属性。

<u>期待される結果</u>:

商品は正しい順序で返されます。 製品を複数の属性で並べ替えても機能します。

<u>実際の結果</u>:

商品が正しい順序で返されません。 製品を複数の属性で並べ替えても機能しません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。

