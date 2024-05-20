---
title: 「ACSD-48587:HTMLキャラクターを含む SKU で product ウィジェットが機能しない」
description: ACSD-48587 パッチを適用すると、products ウィジェットのマッチングルール内のHTMLの特殊文字によって、一致する商品が表示されないAdobe Commerceの問題を修正できます。
exl-id: 9f8f436c-f3ef-4510-a941-12f701e7524e
feature: Admin Workspace, CMS, Orders, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# ACSD-48587:HTMLキャラクターを含む SKU で product ウィジェットが機能しない

ACSD-48587 パッチでは、products ウィジェットのマッチングルール内のHTMLの特殊文字によって、一致する商品が表示されない問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされています。 パッチ ID は ACSD-48587 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品ウィジェットが、を含む SKU で機能しない *「&amp;」* シンボル。

<u>再現手順</u>:

1. を含む製品の作成 *「&amp;」* SKU 内（例：s000&amp;01）。
1. で CMS ページのコンテンツを編集する *ページビルダー*.
1. 製品ウィジェットを追加します。
1. ウィジェットを編集して設定 **[!UICONTROL Select Products by]** = **[!UICONTROL SKU]**.
1. 次を含む SKU を入力 *「&amp;」* 「製品 SKU」フィールドに移動します。
1. コンテンツと CMS ページを保存します。
1. を確認します *CMS ページ* のコンテンツ *ページビルダーのプレビュー* および製品ストアフロント。

<u>期待される結果</u>:

を含む製品 *「&amp;」* sku のがページビルダーのプレビューとストアフロントに表示されます。

<u>実際の結果</u>:

を含む製品 *「&amp;」* SKU 内のは、ページビルダーのプレビューには表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
