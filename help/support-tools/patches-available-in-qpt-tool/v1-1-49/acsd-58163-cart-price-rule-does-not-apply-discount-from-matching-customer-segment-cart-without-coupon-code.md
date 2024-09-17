---
title: 「ACSD-58163：クーポンコードのない買 [!UICONTROL Cart Price Rule] 物かごとの一致から [!UICONTROL Customer Segment] 割引が適用されない」
description: ACSD-58163 パッチを適用すると、クーポンコードのない一致する [!UICONTROL Customer Segment] い買い物かごからのゲストに対して [!UICONTROL Cart Price Rule] が割引を適用しないAdobe Commerceの問題が修正されます。
feature: Products
role: Admin, Developer
source-git-commit: 7603a482953dc0ac0784ab6e6d3b22e4245e3e75
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# ACSD-58163：クーポンコードのない買 [!UICONTROL Cart Price Rule] 物かごとの一致から [!UICONTROL Customer Segment] 割引は適用されません

ACSD-58163 パッチは、クーポンコードがない場合に、[!UICONTROL Cart Price Rule] が一致する [!UICONTROL Customer Segment] カートからの割引を適用しない問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.49 がインストールされている場合に使用できます。 パッチ ID は ACSD-58163 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p7

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クーポンコード [!UICONTROL Cart Price Rule] ない場合、一致する [!UICONTROL Customer Segment] 買い物かごからのゲストに対する割引は適用されません。

<u> 再現手順 </u>:

1. 顧客セグメントを作成：
   * 訪問者のために。
   * 買い物かごに 1 つの製品が入っていることを条件として。

1. *[!UICONTROL Cart Price Rule]* を作成します。
   * クーポンコードなし。
   * 訪問者の顧客セグメントと一致する条件を指定します。

1. シンプルな製品を作成します。
1. ゲストとしてストアフロントを開きます。
1. シンプルな製品を 1 つ買い物かごに追加します。
1. 買い物かごに移動します。

<u> 期待される結果 </u>:

割引 *[!UICONTROL Cart Price Rule]* 適用されます。

<u> 実際の結果 </u>:

割引 *[!UICONTROL Cart Price Rule]* 適用されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
