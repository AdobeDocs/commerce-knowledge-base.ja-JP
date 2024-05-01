---
title: 「ACSD-49370:GraphQL スキーマの Product 属性に「FilterMatchTypeInput」タイプがある」
description: ACSD-49370 パッチを適用して、GraphQL スキーマで product 属性に「FilterMatchTypeInput」タイプが含まれているAdobe Commerceの問題を修正してください。
exl-id: 132eee3a-30b0-4810-b2f0-0d05d0a9f009
feature: Admin Workspace, Attributes, GraphQL, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# ACSD-49370：製品属性に `FilterMatchTypeInput` GraphQL スキーマに入力

ACSD-49370 パッチは、製品属性にが含まれている問題を修正します `FilterMatchTypeInput` GraphQL スキーマにと入力します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされています。 パッチ ID は ACSD-49370 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品属性にはが含まれます。 `FilterMatchTypeInput` GraphQL スキーマにと入力します。

<u>再現手順</u>:

1. 作成 *日付および時刻* 製品属性。

   * [!UICONTROL Type]: [!UICONTROL DateTime]
   * [!UICONTROL Default Label]: [!UICONTROL Date Time]
   * [!UICONTROL Use in Search]: [!UICONTROL Yes]
   * [!UICONTROL Visible in Advanced Search]: [!UICONTROL Yes]

1. をクエリ *GQL API* のドキュメント `ProductAttributeFilterInput` 型定義。
1. 作成した属性の入力タイプを確認します。

<u>期待される結果</u>:

この *日時* 属性は、フィルターの入力タイプを示します `FilterRangeTypeInput`.

<u>実際の結果</u>:

この *日時* 属性は、フィルターの入力タイプを示します `FilterMatchInputType`.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
