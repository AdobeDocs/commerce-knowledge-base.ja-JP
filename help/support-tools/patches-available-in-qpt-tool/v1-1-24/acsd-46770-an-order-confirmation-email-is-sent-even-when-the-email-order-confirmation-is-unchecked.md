---
title: 「ACSD-46770:[!UICONTROL Email Order Confirmation] がオフの場合でも注文確認メールが送信される」
description: '[!UICONTROL Email Order Confirmation] が選択されていない場合でも注文確認メールが送信されるAdobe Commerceの問題を修正するために、ACSD-46770 パッチを適用してください。'
exl-id: 9cbf3a57-1f59-4030-b432-0e6cad410a27
feature: Communications, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# ACSD-46770:**[!UICONTROL Email Order Confirmation]** がオフの場合でも注文確認メールが送信される

ACSD-46770 パッチは、**[!UICONTROL Email Order Confirmation]** が選択されていない場合でも、ゲストユーザーとして REST API を介して注文できる問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされている場合に使用できます。 パッチ ID は ACSD-46770 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

選択されていない場合でも、注文確認メール **[!UICONTROL Email Order Confirmation]** 送信されます。

<u> 再現手順 </u>:

1. 顧客アカウントを作成します。
1. **[!UICONTROL Sales]**/**[!UICONTROL Order]** に移動し、「**[!UICONTROL Create New Order]**」をクリックします。
1. 顧客を選択し、商品を注文に追加し、住所を入力し、配送方法と支払い方法を選択します。
1. 注文を送信する前に、[**[!UICONTROL Email Order confirmation]**] チェック ボックスをオフにします。
1. 「**[!UICONTROL Submit Order]**」をクリックして、注文を作成します。

<u> 期待される結果 </u>:

**[!UICONTROL Email Order Confirmation]** の選択が解除されている場合は、注文確認メールを送信しないでください。

<u> 実際の結果 </u>:

選択されていない **[!UICONTROL Email Order Confirmation]** チェックボックスにかかわらず、注文確認メールが送信されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
