---
title: 「ACSD-55610：部分的にキャンセルされた注文の割引額が正しくありません」
description: ACSD-55610 パッチを適用すると、一部キャンセルされた注文に間違った割引額が含まれるAdobe Commerceの問題を修正できます。
feature: Invoices, Orders, Price Rules, Shopping Cart
role: Admin, Developer
exl-id: f4cca4fa-dc04-4c86-9176-c648b1d0e732
source-git-commit: c903360ffb22f9cd4648f6fdb4a812cb61cd90c5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# ACSD-55610：部分的にキャンセルされた注文の割引額が正しくありません

ACSD-55610 パッチは、部分的にキャンセルされた注文に誤った割引額がある問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.43 がインストールされている場合に使用できます。 パッチ ID は ACSD-55610 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的にキャンセルされた注文に間違った割引額があります。

<u> 再現手順 </u>:

1. 買い物かご価格ルールを作成します。

   * *[!UICONTROL Rule Name]*: *ウィンターセール*
   * *[!UICONTROL Active]* = *はい*
   * *[!UICONTROL Websites]* = *メイン Web サイト*
   * すべての顧客グループを選択します。
   * 特定のクーポンを選択します。
   * *[!UICONTROL Coupon Code]*: *WINTER10*
   * *[!UICONTROL Conditions]*: *[!UICONTROL If ALL of these conditions are TRUE]*: *小計（Excl. 税）は 75* 以上です。
   * *[!UICONTROL Percent of product price discount]* を適用します。
   * *[!UICONTROL Discount Amount]*: *10*
   * *[!UICONTROL Discard subsequent rules]*: *はい*

1. 価格を 100 に設定した 3 つの製品を作成します。
1. 3 つの製品を買い物かごに追加します。
1. クーポンを適用します。
1. 注文します。
1. 注文の 1 つの品目を請求し、それを出荷します。
1. 他の 2 つの項目をキャンセルします。
1. `base_discount_canceled` 列を確認します。

<u> 期待される結果 </u>:

`base_discount_cancelled` の割引額は正しく反映されます。

<u> 実際の結果 </u>:

`base_discount_cancelled` が正しくありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
