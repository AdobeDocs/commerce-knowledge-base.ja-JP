---
title: 「ACSD-51497：ドロップダウンタイプのカスタム属性でカタログページを並べ替えることができない」
description: ACSD-51497 パッチを適用すると、お客様がドロップダウンタイプのカスタム属性でカタログページを並べ替えることができないAdobe Commerceの問題を修正できます。
feature: Attributes, Cache, Catalog Management, Categories
role: Developer
exl-id: 60a4f375-9b9a-4026-9dc7-d9f847a75656
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# ACSD-51497: タイプのカスタム属性でカタログ ページを並べ替えることができません *ドロップダウン*

ACSD-51497 パッチでは、タイプのカスタム属性によってカタログページを並べ替えることができない問題を修正しました *ドロップダウン*. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされています。 パッチ ID は ACSD-51497 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.3.7-p4、2.4.1 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客がタイプのカスタム属性でカタログページを並べ替えることができない *ドロップダウン*.

<u>再現手順</u>

1. 約 6 つのシンプルな製品を作成して、1 つのカテゴリに割り当てます。
1. 製品属性を作成して、リストページで並べ替えオプションとして追加します。

   * に移動 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Add New Attribute]**.
   * が含まれる **[!UICONTROL Properties]** タブで、以下を設定します。

      * *[!UICONTROL Default Label]* = *テスト*
      * *[!UICONTROL Catalog Input Type]* ストア所有者= *ドロップダウン*
      * *[!UICONTROL Options]*:

         * *第 1*
         * *第 2*
         * *第 3*
         * *第 4*

   * が含まれる **[!UICONTROL Storefront Properties]** タブで、以下を設定します。

      * *[!UICONTROL Used for sorting in product listing]* = *はい*
      * その他のオプションはすべてのままにします *デフォルト*.

1. を割り当てる *テスト* の属性 *デフォルト* で設定された属性 **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Attribute Set]**.
1. に設定する製品の設定 *テスト* 属性値。

   * SKU: s00001、テスト：4 番目
   * SKU: s00002、テスト：third
   * SKU: s00003、テスト：second
   * SKU: s00004、テスト：最初
   * SKU: s00005、テスト：4 番目
   * SKU: s00006、テスト：third

1. キャッシュの再インデックスとクリア。
1. ストアフロントのカテゴリに移動します。
1. で並べ替え *テスト* 属性。

<u>期待される結果</u>:

商品は以下によって並べ替えられます *テスト* 属性。

<u>実際の結果</u>:

商品は、で並べ替えられていません *テスト* 属性。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
