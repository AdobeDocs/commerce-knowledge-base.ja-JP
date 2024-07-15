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

# ACSD-51497: カタログページをタイプ *ドロップダウン* のカスタム属性で並べ替えることができない

ACSD-51497 パッチでは、顧客がタイプ *ドロップダウン* のカスタム属性でカタログページを並べ替えることができない問題を修正しました。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.33 がインストールされている場合に使用できます。 パッチ ID は ACSD-51497 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.3.7-p4、2.4.1 ～ 2.4.6-p1

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

顧客がタイプ *ドロップダウン* のカスタム属性でカタログページを並べ替えることができない。

<u> 再現手順 </u>

1. 約 6 つのシンプルな製品を作成して、1 つのカテゴリに割り当てます。
1. 製品属性を作成して、リストページで並べ替えオプションとして追加します。

   * **[!UICONTROL Admin]**/**[!UICONTROL Stores]**/**[!UICONTROL Attributes]**/**[!UICONTROL Add New Attribute]** に移動します。
   * 「**[!UICONTROL Properties]**」タブで以下を設定します。

      * *[!UICONTROL Default Label]* = *test*
      * ストア所有者の *[!UICONTROL Catalog Input Type]* = *ドロップダウン*
      * *[!UICONTROL Options]*:

         * *first*
         * *秒*
         * *3 番目*
         * *4 番目*

   * 「**[!UICONTROL Storefront Properties]**」タブで以下を設定します。

      * *[!UICONTROL Used for sorting in product listing]* = *はい*
      * その他のオプションはすべて *デフォルト* のままにします。

1. **[!UICONTROL Admin]** > **[!UICONTROL Stores]** > **[!UICONTROL Attributes]** > **[!UICONTROL Attribute Set]** で設定した *デフォルト* 属性に *test* 属性を割り当てます。
1. *test* 属性値を持つように製品を設定します。

   * SKU: s00001、テスト：4 番目
   * SKU: s00002、テスト：third
   * SKU: s00003、テスト：second
   * SKU: s00004、テスト：最初
   * SKU: s00005、テスト：4 番目
   * SKU: s00006、テスト：third

1. キャッシュの再インデックスとクリア。
1. ストアフロントのカテゴリに移動します。
1. *test* 属性で並べ替えます。

<u> 期待される結果 </u>:

製品は *test* 属性で並べ替えられます。

<u> 実際の結果 </u>:

製品は、*test* 属性で並べ替えられていません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
