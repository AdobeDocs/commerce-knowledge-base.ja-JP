---
title: 「ACSD-51204：商品がクレジットメモの作成後に在庫として返されない」
description: ACSD-51204 パッチを適用すると、クレジットメモを作成した後、商品が在庫に戻らないAdobe Commerceの問題を修正できます。
feature: Orders, Products, Returns
role: Admin
exl-id: 302033bc-2ca5-40d6-b692-24ae46b21c31
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# ACSD-51204：クレジットメモを作成した後、商品が在庫に戻らない

ACSD-51204 パッチは、クレジットメモを作成した後、製品が在庫に戻らない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.32 がインストールされています。 パッチ ID は ACSD-51204 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

売り切れた商品は、クレジットメモを作成した後、在庫として返されません。

<u>再現手順</u>:

1. インストール **[!UICONTROL Adobe Commerce]** を有効にします。 **[!UICONTROL Inventory Management Module]** デフォルトで *ソース* および *在庫* のみ。
1. を追加 **[!UICONTROL new product]** ～の量で *10*.
1. 製品をに割り当てます。 **[!UICONTROL default stock]**.
1. ストアフロントで、商品をカートに追加し、利用可能な全数量 10 を注文します。
1. 管理パネルで、を生成します。 *請求書* および *出荷* 注文に対して。
1. を作成 **[!UICONTROL Credit Memo]** （を使用） *再入荷* チェックボックスがすべての項目に対して選択されています。
1. 製品の確認 **[!UICONTROL Salable Quantity]** admin.

<u>期待される結果</u>:

商品の売れる量は～に戻らなければならない *10*.

<u>実際の結果</u>:

製品の販売可能数量は、次のようになります *0*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
