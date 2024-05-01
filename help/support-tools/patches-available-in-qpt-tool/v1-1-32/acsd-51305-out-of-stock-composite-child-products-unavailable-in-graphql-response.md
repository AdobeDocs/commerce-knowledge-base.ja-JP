---
title: 「ACSD-51305:GraphQL応答で使用できない在庫切れの複合子製品」
description: ACSD-51305 パッチを適用して、Adobe Commerceの応答で在庫切れの複合子製品を使用できないGraphQLの問題を修正してください。
exl-id: 0f33eb62-dfd3-4d07-b095-9ee6e9983c4d
feature: Categories, GraphQL, Orders, Products
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# ACSD-51305:GraphQL応答で使用できない在庫切れの複合子製品

ACSD-51305 パッチでは、在庫切れの複合子製品がGraphQL応答で使用できない問題を修正しています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされています。 パッチ ID は ACSD-51305 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの複合子製品は、GraphQL応答では使用できません。

<u>再現手順</u>:

1. 管理者 Web サイトにログインします。
1. カテゴリ（cat1、id=3）を作成します。
1. を作成 *simple1* 製品（在庫切れ、個別に表示されない、割り当て先） *cat1*）に設定します。
1. を作成 *simple2* 製品（在庫あり、個別に表示されず、割り当て先 *cat1*）に設定します。
1. を作成 *bundle1* 次を含む製品 *simple1* および *simple2* ラジオボタンとしての子製品 *オプション 1* 製品とを、に割り当てます *cat1* カテゴリ。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL System]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Inventory]**.

   * を設定 **[!UICONTROL Display Out of Stock Products]** 対象： *はい*.

1. を開きます *bundle1* ストアフロントに製品を配置し、その両方を確保します *simple1* および *simple2* その中に子製品が表示されます。
1. 次のGraphQL クエリを実行します。

   ```GraphQL
   {
       categoryList(filters: { ids: { in: ["3"] } }) {
           id
           name
           products(pageSize: 8, sort: { position: ASC }) {
               total_count
               items {
                   id
                   sku
                   name
                   ... on BundleProduct {
                       url_key
                       items {
                           title
                           sku
                           options {
                               quantity
                               position
                               is_default
                               product {
                                   id
                                   name
                                   sku
                               }
                           }
                       }
                   }
               }
           }
       }
   }
   ```

<u>期待される結果</u>:

この **[!UICONTROL Product]** 内のセクション **[!UICONTROL Options]** ブロックが空ではありません。

<u>実際の結果</u>:

この **[!UICONTROL Product]** 内のセクション **[!UICONTROL Options]** ブロックが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
