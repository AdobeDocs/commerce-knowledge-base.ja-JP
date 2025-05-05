---
title: 「ACSD-46581：買い物かごで国を選択した後、推定税合計が更新されない」
description: ACSD-46581 パッチを適用すると、買い物かごで国を切り替えても税率が更新されないAdobe Commerceの問題を解決できます。
exl-id: 17334f7b-e5a2-4091-8196-eff80875c003
feature: Orders, Shopping Cart
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# ACSD-46581：買い物かごで国を選択した後、推定税合計が更新されない

この ACSD-46581 パッチは、買い物かごで国を切り替えても税率が更新されない問題を解決します。 出荷方法を選択した後にのみ更新されます。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.21 がインストールされている場合に使用できます。 パッチ ID は ACSD-46581 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**
* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

買い物かごで国を切り替えても、税率が更新されない。

<u> 再現手順 </u>:

1. Adobe Commerce管理者で、**[!UICONTROL Stores]**/**[!UICONTROL Tax Zone and Rates]** に移動します。
1. **[!UICONTROL Country]** = _米国_、**[!UICONTROL State]** = _*_、**[!UICONTROL Rate]** = _8.25_ の新しい税率を作成します。
1. **[!UICONTROL Country]** = _インド_、**[!UICONTROL State]** = _*_、**[!UICONTROL Rate]** = _10_ の新しい税率を作成します。
1. 米国とインドの両方の税率を使用して税務処理基準を作成します。
1. **[!UICONTROL Configuration]**/**[!UICONTROL Sales]**/**[!UICONTROL Shipping Methods]** に移動し、複数の発送方法（_定額_ および _送料無料_ など）を有効にします。
1. **[!UICONTROL Taxable Goods]** 税クラスを持つシンプルな製品を作成します。
1. 商品を店舗正面の買い物かごに追加します。
1. 買い物かごを開いて、税額を確認します。
1. 米国のデフォルトの税金設定が適用され、8.25% の税率に基づいて税金が計算されます。
1. 国をインドに切り替えなさい。

<u> 期待される結果 </u>:

インドに切り替えると 10% に変わりました。

<u> 実際の結果 </u>:

買い物かごの合計セクションの税額は同じままです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
