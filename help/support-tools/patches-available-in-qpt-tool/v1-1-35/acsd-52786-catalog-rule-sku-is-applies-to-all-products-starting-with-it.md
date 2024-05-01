---
title: '''ACSD-52786: カタログルール *[!UICONTROL SKU is]*SKU で始まるすべての製品に適用'
description: ACSD-52786 パッチを適用して、カタログのルールの条件*が存在するAdobe Commerceの問題を修正してください[!UICONTROL SKU is]*は、特定の SKU で始まるすべての製品に適用されます。
feature: Price Rules
role: Admin
exl-id: af373b6c-5944-412b-a544-cc6fc3f209d3
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# ACSD-52786: カタログルール &quot;*[!UICONTROL SKU is]*」は、SKU で始まるすべての製品に適用されます

ACSD-52786 パッチは、カタログルールの条件が適用される問題を修正します *[!UICONTROL SKU is]* 特定の SKU で始まるすべての製品に適用されます。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされています。 パッチ ID は ACSD-52786 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カタログルールの条件 *[!UICONTROL SKU is]* 特定の SKU で始まるすべての製品に適用されます。

<u>再現手順</u>:

1. SKU が「24」の製品と SKU が「24-MB01」の製品の 2 つを作成します。
1. に移動します。 **[!UICONTROL Marketing]** > **[!UICONTROL Catalog Price Rule]** > **[!UICONTROL Add New Rule]**.
1. 次の条件を適用します。
   * *[!UICONTROL If **&#x200B;すべて&#x200B;**これらの条件の一部は次のとおりです** TRUE **]*: *[!UICONTROL SKU is 24]*
1. アクションで割引金額を設定します。
1. クリック **[!UICONTROL Save and Apply]**.
1. キャッシュをフラッシュします。
1. ストアフロントに移動し、24-MB01 の価格を確認してください。

<u>期待される結果</u>:

カタログルールは、SKU が 24 の 1 つの製品にのみ適用されます。

<u>実際の結果</u>:

カタログルールの条件 *[!UICONTROL SKU is]* 特定の SKU で始まるすべての製品に適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
