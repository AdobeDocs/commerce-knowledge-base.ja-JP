---
title: 「ACSD-52824：会社の顧客に対して表示される支払い方法が無効」
description: Adobe Commerceの問題を修正するために ACSD-52824 パッチを適用してください。この問題の場所は次のとおりです。 [!DNL PayPal Express], [!DNL Google Pay], and [!DNL Apple Pay] 会社設定で無効になっているにもかかわらず、会社の顧客に対して支払い方法が表示されます。
feature: Payments, B2B, Shopping Cart
role: Admin, Developer
exl-id: 03496fb1-d492-4f02-9cdc-466cb571a2eb
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# ACSD-52824：会社の顧客に対して無効な支払方法が表示される

ACSD-52824 パッチは、次の問題を修正します。 [!DNL PayPal Express], [!DNL Google Pay]、および [!DNL Apple Pay] 会社設定で無効になっているにもかかわらず、会社の顧客に対して支払い方法が表示されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.45 がインストールされています。 パッチ ID は ACSD-52824 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

無効な支払い方法は、会社の顧客に対して表示されます。

<u>再現手順</u>:

1. の設定と有効化 [!DNL PayPal Express Checkout]. に移動します。 **[!UICONTROL Basic Settings]** > を選択 **[!DNL PayPal Express Checkout]** オプションを設定します **[!UICONTROL Display on Shopping Cart]** 対象： *はい*.
1. 設定 [!DNL Braintree] および有効化 [!DNL Apple Pay] および [!DNL Google Pay] から [!DNL Braintree].
1. に移動します。 **[!UICONTROL Customers]** > **[!UICONTROL Companies]** 新しい会社を作成します。
1. クリックする **[!UICONTROL Advanced Settings]**&#x200B;を見つけます。 **[!UICONTROL Applicable Payment Methods]** を選択します **[!UICONTROL Selected Payment Methods]**.
1. 次の下 **[!UICONTROL Selected Payment Methods]**、有効でに関連付けられていない支払方法を選択します *[!DNL PayPal Express Checkout]*, *[!DNL Apple Pay]*、または *[!DNL Google Pay]*. 例えば、 **[!UICONTROL Check/Money Order]**.
1. 適切な支払い方法を選択した後、新しい顧客を作成し、以前に作成した会社に関連付けます。
1. 会社に関連付けられている顧客アカウントでログインし、買い物かごへの商品の追加に進みます。
1. チェックアウトプロセス中のミニカート、買い物かご、支払い手順に注意してください。

<u>期待される結果</u>:

からの支払いオプション [!DNL PayPal] および [!DNL Braintree] ミニ カートと買い物かごには表示されません。

<u>実際の結果</u>:

からの支払いオプション [!DNL PayPal] および [!DNL Braintree] ミニカートと買い物かごに表示されたままになります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
