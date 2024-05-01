---
title: 「ACSD-46581：買い物かごで国を選択した後、推定税合計が更新されない」
description: ACSD-46581 パッチを適用すると、買い物かごで国を切り替えても税率が更新されないAdobe Commerceの問題を解決できます。
exl-id: 17334f7b-e5a2-4091-8196-eff80875c003
feature: Orders, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# ACSD-46581：買い物かごで国を選択した後、推定税合計が更新されない

この ACSD-46581 パッチは、買い物かごで国を切り替えても税率が更新されない問題を解決します。 出荷方法を選択した後にのみ更新されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされています。 パッチ ID は ACSD-46581 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

買い物かごで国を切り替えても、税率が更新されない。

<u>再現手順</u>:

1. Adobe Commerce Admin で、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Tax Zone and Rates]**.
1. に対する新しい税率の作成 **[!UICONTROL Country]** = _米国_, **[!UICONTROL State]** = _*_, **[!UICONTROL Rate]** = _8.25_.
1. に対する新しい税率の作成 **[!UICONTROL Country]** = _インド_, **[!UICONTROL State]** = _*_, **[!UICONTROL Rate]** = _10_.
1. 米国とインドの両方の税率を使用して税務処理基準を作成します。
1. に移動 **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Shipping Methods]** 複数の発送方法を有効にする（_定額料金_ および _送料無料_ （例：）。
1. を使用したシンプルな製品の作成 **[!UICONTROL Taxable Goods]** 税クラス。
1. 商品を店舗正面の買い物かごに追加します。
1. 買い物かごを開いて、税額を確認します。
1. 米国のデフォルトの税金設定が適用され、8.25% の税率に基づいて税金が計算されます。
1. 国をインドに切り替えなさい。

<u>期待される結果</u>:

インドに切り替えると 10% に変わりました。

<u>実際の結果</u>:

買い物かごの合計セクションの税額は同じままです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、次を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
