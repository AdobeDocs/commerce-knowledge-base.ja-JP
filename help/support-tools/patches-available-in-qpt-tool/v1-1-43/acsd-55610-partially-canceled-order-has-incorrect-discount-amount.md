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

ACSD-55610 パッチは、部分的にキャンセルされた注文に誤った割引額がある問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.43 がインストールされています。 パッチ ID は ACSD-55610 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.6-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

部分的にキャンセルされた注文に間違った割引額があります。

<u>再現手順</u>:

1. 買い物かご価格ルールを作成します。

   * *[!UICONTROL Rule Name]*: *冬物販売*
   * *[!UICONTROL Active]* = *はい*
   * *[!UICONTROL Websites]* = *メイン Web サイト*
   * すべての顧客グループを選択します。
   * 特定のクーポンを選択します。
   * *[!UICONTROL Coupon Code]*: *冬 10*
   * *[!UICONTROL Conditions]*: *[!UICONTROL If ALL of these conditions are TRUE]*: *小計 税）が 75 以上*
   * 適用 *[!UICONTROL Percent of product price discount]*.
   * *[!UICONTROL Discount Amount]*: *10*
   * *[!UICONTROL Discard subsequent rules]*: *はい*

1. 価格を 100 に設定した 3 つの製品を作成します。
1. 3 つの製品を買い物かごに追加します。
1. クーポンを適用します。
1. 注文します。
1. 注文の 1 つの品目を請求し、それを出荷します。
1. 他の 2 つの項目をキャンセルします。
1. を確認します `base_discount_canceled` 列。

<u>期待される結果</u>:

割引金額 `base_discount_cancelled` 正しく反映されます。

<u>実際の結果</u>:

この `base_discount_cancelled` が正しくありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
