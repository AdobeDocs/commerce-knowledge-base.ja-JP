---
title: 「ACSD-49839：共有カタログの価格と構造がエラーをスロー」
description: ACSD-49839 パッチを適用すると、商品の SKU に一重引用符または二重引用符が含まれている場合、共有カタログの価格と構造が管理者でエラーをスローするAdobe Commerceの問題を修正できます。
exl-id: 4c477ae8-602b-452e-83f0-b72a29547ef9
feature: Admin Workspace, Catalog Management, Categories
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# ACSD-49839：共有カタログの価格と構造がエラーをスロー

製品の SKU に一重引用符または二重引用符が含まれている場合、共有カタログの価格と構造が管理者でエラーをスローする問題が、ACSD-49839 パッチで修正されました。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-49839 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品の SKU に一重引用符または二重引用符が含まれている場合、共有カタログの価格と構造により、管理者でエラーがスローされる。

<u>再現手順</u>:

1. 特殊文字（二重引用符など）を使用して、一部の製品 SKU を設定します。
   *[Product&quot;12, Product&quot;14, Product&quot;15]*.
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Catalog]** > **[!UICONTROL Shared Catalog]** > **[!UICONTROL Add Shared Catalog]** （例：）*[共有カタログのテスト]*）に設定します。
1. すべて割り当て **[!UICONTROL Products and Categories]** > **[!UICONTROL Generate Catalog]** > **[!UICONTROL Save]**.
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Catalog]** > **[!UICONTROL Shared Catalog]** > **[!UICONTROL Test Shared Catalog]** > **[!UICONTROL Action]** > **[!UICONTROL Set Pricing and Structure]**.
1. マーク *[!UICONTROL Root Catalog]* をクリックして、すべてのカテゴリと製品を選択します。
1. ネットワークパネルでAJAX リクエストを確認します。

<u>期待される結果</u>:

製品の SKU に一重引用符または二重引用符が含まれている場合、共有カタログの価格と構造で、管理者にエラーが表示されない。

<u>実際の結果</u>:

製品の SKU に一重引用符または二重引用符が含まれている場合、共有カタログの価格と構造により、管理者にエラーが発生する。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
