---
title: 「ACSD-56090:GraphQL応答がストアに固有ではありません」
description: ACSD-56090 パッチを適用すると、GraphQL応答にストア固有のデータではなく、すべてのストアデータが含まれるAdobe Commerceの問題が修正されます。
feature: GraphQL
role: Admin, Developer
exl-id: 129491e0-1a77-4ccc-8aba-cd0afdb26176
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# ACSD-56090:GraphQL応答がストアに固有ではない

ACSD-56090 パッチは、GraphQLの応答に、ストア固有のデータではなく、すべてのストアデータが含まれる問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-56090 です。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

GraphQL応答に、ストア固有のデータではなく、すべてのストアデータが含まれる。

<u> 再現手順 </u>:

1. **[!UICONTROL Admin panel]**/**[!UICONTROL Catalog]**/**[!UICONTROL Categories]** にログインし、2 つのルートカテゴリを作成します。
1. 各ルートカテゴリには、1 つのサブカテゴリが必要です。
1. **[!UICONTROL Stores]**/**[!UICONTROL All stores]**/に移動します。2 つのストアが存在し、それぞれについてルートカテゴリが異なります。 （各ストアには、少なくとも 1 つのストア表示が必要）
1. **[!UICONTROL Catalog]**/**[!UICONTROL Products]**/製品を作成に移動します。

* 割り当てられたすべてのルートカテゴリとサブカテゴリ
* 割り当てられたすべての Web サイト。

1. GraphqQL クエリを実行します（ヘッダーを追加 – store = &#39;storename）。

```
   query {
     products(filter: { url_key: { eq: "abc" } }) {
       items {
         categories {
           name
           id
           url_path
           breadcrumbs {
             category_id
             category_name
             category_level
           }
         }
       }
     }
   }
```

1. GraphqQL クエリを実行した後、応答を確認します。

<u> 期待される結果 </u>:

ストア固有のデータが返されます

<u> 実際の結果 </u>:

返されるデータは、ストアに固有のものではありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
