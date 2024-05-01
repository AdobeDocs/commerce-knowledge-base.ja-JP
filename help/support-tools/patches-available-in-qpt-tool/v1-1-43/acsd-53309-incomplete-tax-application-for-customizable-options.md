---
title: 「ACSD-53309：カスタマイズ可能なオプションの不完全な税金適用および [!UICONTROL Regular Price] ラベル`
description: ACSD-53309 パッチを適用して、「」に税金が完全には適用されないAdobe Commerceの問題を修正してください[!UICONTROL Regular Price]カスタマイズ可能なオプションが選択された場合の「ラベル。
feature: Taxes, Shipping/Delivery
role: Admin, Developer
exl-id: de9b151e-6f92-4231-9e9f-4818c2961782
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# ACSD-53309：カスタマイズ可能なオプションおよび「」の不完全な税金適用[!UICONTROL Regular Price]ラベル

ACSD-53309 パッチは、「」で税金が完全に適用されない問題を修正しました[!UICONTROL Regular Price]カスタマイズ可能なオプションが選択された場合の「ラベル。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.43 がインストールされています。 パッチ ID は ACSD-53309 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

税金が「」に完全に反映されていません[!UICONTROL Regular Price]カスタマイズ可能なオプションが選択された場合の「ラベル。

<u>再現手順</u>:

1. 管理パネルにログインします。
1. に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Tax]** 税金設定を構成します。

   * [!UICONTROL Tax Classes]:

      * [!UICONTROL Tax Class for Shipping] = [!UICONTROL Taxable Goods]
      * [!UICONTROL Tax Class for Gift Options] = [!UICONTROL Taxable Goods]

   * [!UICONTROL Calculation Settings]:

      * [!UICONTROL Catalog Prices] = [!UICONTROL Including Tax]
      * [!UICONTROL Shipping Prices] = [!UICONTROL Including Tax]
      * [!UICONTROL Apply Discount On Prices] = [!UICONTROL Including Tax]

   * [!UICONTROL Default Tax Destination Calculation]:

      * [!UICONTROL Default Post Code] = *

   * [!UICONTROL Price Display Settings]:

      * [!UICONTROL Display Product Prices In Catalog] = [!UICONTROL Including Tax]
      * [!UICONTROL Display Shipping Prices] = [!UICONTROL Including Tax]

   * [!UICONTROL Shopping Cart Display Settings]:

      * [!UICONTROL Display Prices] = [!UICONTROL Including Tax]
      * [!UICONTROL Display Subtotal] = [!UICONTROL Including Tax]
      * [!UICONTROL Display Shipping Amount] = [!UICONTROL Including Tax]

1. を設定 **[!UICONTROL Shipping Settings]** > **[!UICONTROL Origin]** > **[!UICONTROL Country]** = *英国*.

1. 以下を作成します *[!UICONTROL Tax Rate]* および *[!UICONTROL Tax Rules]*:

   * [!UICONTROL Country] =米国
   * [!UICONTROL Zip Code] = *
   * [!UICONTROL State] = *
   * [!UICONTROL Rate] = 20%
1. シンプルな製品を作成し、以下を設定します。
   * [!UICONTROL Price = 110]
   * [!UICONTROL Special Price = 100]
   * ドロップダウンで、「タイプ」を「カスタムオプション」に設定し、価格を 15% に設定します
1. ストアフロントで作成されたシンプルなアイテムの製品ページに移動します。
1. 作成したカスタムオプションを選択します。 *15%*.

<u>期待される結果</u>:

* 選択したカスタムオプションに 20% の税金が適用されます。
* &#39;[!UICONTROL Regular Price]&#39; = 151.80。

<u>実際の結果</u>:

* 選択したカスタムオプションには 20% の税金は適用されません。
* &#39;[!UICONTROL Regular Price]&#39; = 148.50。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
