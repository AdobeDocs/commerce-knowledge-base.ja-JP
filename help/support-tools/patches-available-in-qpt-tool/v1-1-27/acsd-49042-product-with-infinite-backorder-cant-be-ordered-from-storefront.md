---
title: 「ACSD-49042：順不同の商品はストアフロントから注文できない」
description: ACSD-49042 パッチを適用すると、順不同の商品をストアフロントから注文できないAdobe Commerceの問題を修正できます。
exl-id: b9227296-f300-447c-a241-30ccc0691c9a
feature: Admin Workspace, Orders, Products, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# ACSD-49042：順不同の商品はストアフロントからは注文できません

ACSD-49042 パッチでは、順不同の商品をストアフロントから注文できない問題を修正しました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.27 がインストールされています。 パッチ ID は ACSD-49042 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.4-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

このエラーは、順不同の商品をストアフロントから注文できない場合に発生します。

<u>再現手順</u>:

1. 次の設定を行います。
   * **[!UICONTROL Display Out of Stock Products]** をに設定 *[!UICONTROL Yes]*.
   * **[!UICONTROL Backorders]** をに設定 *[!UICONTROL Allow Qty Below 0]*.
1. 新しいを追加 **[!DNL custom stock]** および **[!DNL custom source]**.
1. への製品の割り当て **[!DNL custom source]** また、そのための在庫番号が設定されていることを確認します（例： *10*）に設定します。
1. 製品の編集ページで、を開きます。 **[!UICONTROL Advanced Inventory]**. を **[!UICONTROL minimum quantity]** 買い物かご内（例： *160*）に設定します。 数量は在庫より上である必要があります。
1. 店頭に移動し、商品を購入して予約を作成します。
1. 変更： **[!UICONTROL product quantity]** 対象： *0*. 重要なポイントは、 **[!DNL Admin panel]** 予約がある場合。
1. を開きます **[!UICONTROL product page]** ストアフロントで、商品をカートに追加してみてください。

<u>期待される結果</u>:

以下の数量のバックオーダーがあるので、カートに製品を追加できます *0* 許可されています。

<u>実際の結果</u>:

商品が在庫切れと表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
