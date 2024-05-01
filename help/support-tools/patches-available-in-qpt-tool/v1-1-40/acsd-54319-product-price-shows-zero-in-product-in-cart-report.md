---
title: '''ACSD-54319：製品価格がゼロと表示される*[!UICONTROL Products in Carts]* レポート`'
description: ACSD-54319 パッチを適用して、*で製品価格がゼロと表示されるAdobe Commerceの問題を修正してください[!UICONTROL Products in Carts]* レポート
feature: Reporting, Products
role: Admin, Developer
exl-id: f53b3ed3-d5d5-461c-bba2-4f9f3f038580
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# ACSD-54319：製品価格が 0 と表示される *[!UICONTROL Products in Carts]* 報告書

ACSD-54319 パッチは、で製品価格が 0 と表示される問題を修正します。 *[!UICONTROL Products in Carts]* レポート。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.40 がインストールされています。 パッチ ID は ACSD-54319 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品価格はでゼロと表示されます *[!UICONTROL Products in Carts]* レポート。

<u>再現手順</u>:

1. を設定 **[!UICONTROL Catalog Price Scope]** 対象： **[!UICONTROL Website]** から **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog]** > **[!UICONTROL Price]** > **[!UICONTROL Catalog Price Scope]**.
1. から 2 つ目の web サイトを作成します **[!UICONTROL Stores]** > **[!UICONTROL All Stores]**.
1. 商品の作成元 **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.
1. この製品を 2 番目の web サイトにのみ割り当てます。
1. 2 番目の web サイトから買い物かごに製品を追加します。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Reports]** > **[!UICONTROL Marketing]** > **[!UICONTROL Products In Carts]** グリッド。
1. を確認します *[!UICONTROL Price]* 列： *[!UICONTROL Products In Carts]* グリッド。

<u>期待される結果</u>:

製品価格がゼロではありません *[!UICONTROL Products in Carts]* レポートグリッド。

<u>実際の結果</u>:

製品価格はでゼロです *[!UICONTROL Products in Carts]* レポートグリッド。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
