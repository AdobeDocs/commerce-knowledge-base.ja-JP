---
title: 'ACSD-52786：カタログルール *[!UICONTROL SKU is]*は、SKU で始まるすべての製品に適用されます'
description: ACSD-52786 パッチを適用すると、特定の SKU で始まるすべての商品にカタログルール条件*[!UICONTROL SKU is]*が適用されるAdobe Commerceの問題が修正されます。
feature: Price Rules
role: Admin
exl-id: af373b6c-5944-412b-a544-cc6fc3f209d3
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# ACSD-52786：カタログルール「*[!UICONTROL SKU is]*」は、SKU で始まるすべての製品に適用されます

ACSD-52786 パッチでは、特定の SKU で始まるすべての製品にカタログルールの条件 *[!UICONTROL SKU is]* が適用される問題が修正されています。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.35 がインストールされている場合に使用できます。 パッチ ID は ACSD-52786 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.5-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カタログルールの条件 *[!UICONTROL SKU is]*、特定の SKU で始まるすべての製品に適用されます。

<u> 再現手順 </u>:

1. SKU が「24」の製品と SKU が「24-MB01」の製品の 2 つを作成します。
1. **[!UICONTROL Marketing]**/**[!UICONTROL Catalog Price Rule]**/**[!UICONTROL Add New Rule]** に移動します。
1. 次の条件を適用します。
   * 次の条件の *[!UICONTROL If **&#x200B; すべて &#x200B;** は**&#x200B; TRUE &#x200B;**]*&#x200B;です。*[!UICONTROL SKU is 24]*
1. アクションで割引金額を設定します。
1. 「**[!UICONTROL Save and Apply]**」をクリックします。
1. キャッシュをフラッシュします。
1. ストアフロントに移動し、24-MB01 の価格を確認してください。

<u> 期待される結果 </u>:

カタログルールは、SKU が 24 の 1 つの製品にのみ適用されます。

<u> 実際の結果 </u>:

カタログルールの条件 *[!UICONTROL SKU is]*、特定の SKU で始まるすべての製品に適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
