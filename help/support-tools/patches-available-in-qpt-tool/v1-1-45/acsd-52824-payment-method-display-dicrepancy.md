---
title: 「ACSD-52824：会社の顧客に対して表示される支払い方法が無効」
description: 会社設定で無効になっているにもかかわらず、会社のお客様に支払い方法が表示されるAdobe Commerceの問題を修正するため  [!DNL PayPal Express], [!DNL Google Pay], and [!DNL Apple Pay] ACSD-52824 パッチを適用してください。
feature: Payments, B2B, Shopping Cart
role: Admin, Developer
exl-id: 03496fb1-d492-4f02-9cdc-466cb571a2eb
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ACSD-52824：会社の顧客に対して無効な支払方法が表示される

ACSD-52824 パッチは、会社設定で無効になっているにもかかわらず、会社の顧客に [!DNL PayPal Express]、[!DNL Google Pay]、[!DNL Apple Pay] の支払い方法が表示される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされている場合に使用できます。 パッチ ID は ACSD-52824 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

無効な支払い方法は、会社の顧客に対して表示されます。

<u> 再現手順 </u>:

1. [!DNL PayPal Express Checkout] を設定して有効にします。 **[!UICONTROL Basic Settings]**/**[!DNL PayPal Express Checkout]** を選択に移動し、**[!UICONTROL Display on Shopping Cart]** のオプションを *はい* に設定します。
1. [!DNL Braintree] を設定し、[!DNL Apple Pay] と [!DNL Google Pay] ～ [!DNL Braintree] を有効にします。
1. **[!UICONTROL Customers]**/**[!UICONTROL Companies]** に移動し、新しい会社を作成します。
1. **[!UICONTROL Advanced Settings]** をクリックして **[!UICONTROL Applicable Payment Methods]** を探し、**[!UICONTROL Selected Payment Methods]** を選択します。
1. 「**[!UICONTROL Selected Payment Methods]**」で、有効で、*[!DNL PayPal Express Checkout]*、*[!DNL Apple Pay]* または *[!DNL Google Pay]* に関連付けられていない支払方法を選択します。 例えば、「**[!UICONTROL Check/Money Order]**」を選択します。
1. 適切な支払い方法を選択した後、新しい顧客を作成し、以前に作成した会社に関連付けます。
1. 会社に関連付けられている顧客アカウントでログインし、買い物かごへの商品の追加に進みます。
1. チェックアウトプロセス中のミニカート、買い物かご、支払い手順に注意してください。

<u> 期待される結果 </u>:

[!DNL PayPal] と [!DNL Braintree] の支払いオプションは、ミニカートと買い物かごには表示されません。

<u> 実際の結果 </u>:

[!DNL PayPal] と [!DNL Braintree] の支払いオプションは、ミニ カートとショッピング カートに表示されたままになります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html?lang=ja) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html?lang=ja)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja)」を参照してください。
