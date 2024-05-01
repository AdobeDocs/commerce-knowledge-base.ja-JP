---
title: '''ACSD-46617: **[!UICONTROL Continue to Checkout]小計が設定された最小注文額を超えるとグレー表示される** ボタン'
description: '**のAdobe Commerceの問題を解決するために、ACSD-46617 パッチを適用してください[!UICONTROL Continue to Checkout]小計**設定された最小注文額を超えている場合でも、ボタンはグレー表示されます。'
exl-id: 42fe02bd-f48b-4c6d-8643-ea2c1aa98c94
feature: Checkout, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# ACSD-46617: &quot;[!UICONTROL Continue to Checkout]「」ボタンは小計が「」より大きい場合にグレー表示される[!UICONTROL Minimum Order Amount]“

この ACSD-46617 パッチは、 **[!UICONTROL Continue to Checkout]** 小計が設定された最小注文額を超えている場合でも、ボタンはグレー表示されます。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.24 がインストールされています。 パッチ ID は ACSD-46617 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この **[!UICONTROL Continue to Checkout]** 小計が設定された最小注文額を超えている場合でも、ボタンはグレー表示されます。

<u>再現手順</u>:

1. Adobe Commerce管理者に移動します **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Minimum Order Amount]** を設定して、以下を行います。
   * [!UICONTROL Enable]: *[!UICONTROL Yes]*
   * 
     [!UICONTROL Minimum Amount]: *2*

1. を作成 [!UICONTROL Cart Price Rule].
   * [!UICONTROL Coupon Code]: *[!UICONTROL TEST (optional)]*
   * [!UICONTROL Conditions]: *[!UICONTROL Keep empty]*
   * [!UICONTROL Actions]:
      * [!UICONTROL Apply]: *[!UICONTROL Percent of product price discount]*
      * 
        [!UICONTROL Discount Amount]: *92*
      * [!UICONTROL Apply to Shipping Amount]: *[!UICONTROL Yes]*
1. 価格が 25 ドルの製品を作成します。
1. 商品を買い物かごに追加します。
1. ショッピングカートに移動し、$5 を選択します **[!UICONTROL Flat Rate shipping]** メソッドを実行し、クーポンコードを適用します。
1. チェックアウトに移動し、配送を完了してから、に移動します。 **[!UICONTROL Paytment]** セクション。
1. 買い物かごに戻ります。

<u>期待される結果</u>:

$2.4 の総計が必要な金額$2 を超えているので、最小注文額に関するエラーはありません。

<u>実際の結果</u>:

* $2.4 の総計が最小注文金額$2 よりも大きい場合でも、最小注文金額に関するエラーがあります。
* この **[!UICONTROL Continue to Checkout]** ボタンはグレー表示されています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
