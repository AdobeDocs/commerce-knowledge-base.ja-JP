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

ACSD-51305 パッチでは、在庫切れの複合子製品がGraphQL応答で使用できない問題を修正しています。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされている場合に使用できます。 パッチ ID は ACSD-51305 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6 - 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの複合子製品は、GraphQL応答では使用できません。

<u> 再現手順 </u>:

1. 管理者 Web サイトにログインします。
1. カテゴリ（cat1、id=3）を作成します。
1. *simple1* 製品（在庫切れ、個別に表示されない、*cat1*）に割り当てを作成します。
1. *cat1* に割り当てられた、*simple2* 製品（在庫あり、個別には表示されない）を作成します。
1. *simple1* と *simple2* 子製品を持つ *bundle1* 製品をラジオボタン *option1* 製品として作成して、*cat1* カテゴリに割り当てます。
1. **[!UICONTROL Admin]**/**[!UICONTROL System]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Inventory]** に移動します。

   * **[!UICONTROL Display Out of Stock Products]** を *はい* に設定します。

1. ストアフロントで *bundle1* 製品を開き、*simple1* 子製品と *simple2* 子製品の両方が内部に表示されていることを確認します。
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

<u> 期待される結果 </u>:

**[!UICONTROL Options]** ブロック内の **[!UICONTROL Product]** セクションが空ではありません。

<u> 実際の結果 </u>:

**[!UICONTROL Options]** ブロック内の **[!UICONTROL Product]** セクションが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
