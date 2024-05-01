---
title: 「ACSD-46770：次の場合でも注文確認メールが送信されます [!UICONTROL Email Order Confirmation] チェックをオフにする
description: 次の場合でも注文確認メールが送信されるAdobe Commerceの問題を修正するために、ACSD-46770 パッチを適用してください [!UICONTROL Email Order Confirmation] が選択されていません。
exl-id: 9cbf3a57-1f59-4030-b432-0e6cad410a27
feature: Communications, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# ACSD-46770：次の場合でも注文確認メールが送信されます **[!UICONTROL Email Order Confirmation]** オフ

ACSD-46770 パッチは、次の場合でも、ゲストユーザーとして REST API を使用して注文できる問題を修正しました **[!UICONTROL Email Order Confirmation]** が選択解除されました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-46770 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

次の場合でも注文確認メールが送信されます。 **[!UICONTROL Email Order Confirmation]** が選択されていません。

<u>再現手順</u>:

1. 顧客アカウントを作成します。
1. に移動 **[!UICONTROL Sales]** > **[!UICONTROL Order]** をクリックし、  **[!UICONTROL Create New Order]**.
1. 顧客を選択し、商品を注文に追加し、住所を入力し、配送方法と支払い方法を選択します。
1. 注文を送信する前に、 **[!UICONTROL Email Order confirmation]** チェックボックスをオンにします。
1. クリックする **[!UICONTROL Submit Order]** をクリックして注文を作成します。

<u>期待される結果</u>:

次の場合は、注文確認メールを送信しないでください **[!UICONTROL Email Order Confirmation]** が選択解除されました。

<u>実際の結果</u>:

未選択にかかわらず、注文確認メールが送信されます **[!UICONTROL Email Order Confirmation]** チェックボックスをオンにします。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
