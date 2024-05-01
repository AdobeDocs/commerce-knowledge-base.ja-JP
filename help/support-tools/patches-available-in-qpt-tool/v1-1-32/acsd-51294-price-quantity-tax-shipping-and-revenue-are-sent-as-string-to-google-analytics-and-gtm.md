---
title: 'ACSD-51294：価格、数量、税、送料、文字列としてに送信された売上高 [!DNL Google Analytics] と GTM'
description: ACSD-51294 パッチを適用すると、価格、数量、税、送料、売上高が文字列としてに送信されるAdobe Commerceの問題を修正できます [!DNL Google Analytics] と GTM です。
feature: Orders, Shipping/Delivery, Variables
role: Admin
exl-id: 159e1e98-0def-4b20-901d-f5f58c3ead7c
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# ACSD-51294：価格、数量、税、送料、文字列としてに送信された売上高 [!DNL Google Analytics] および GTM

ACSD-51294 パッチは、価格、数量、税、送料、売上高がに文字列として送信される問題を修正します [!DNL Google Analytics] と GTM です。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされています。 パッチ ID は ACSD-51294 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5 ～ 2.4.6-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

価格、数量、税、送料および売上高は、文字列としてに送信されます。 [!DNL Google Analytics] と GTM です。

<u>再現手順</u>:

1. 設定 [!DNL Google Tag Manager] に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Google API]** > **[!UICONTROL Google GTag]** > **[!UICONTROL Google Analytics4]**.
2. シンプルな製品を作成します。
3. その商品のチェックアウトを完了します。
4. を確認します `dataLayer` チェックアウト成功ページの JavaScript 変数。

<u>期待される結果</u>

価格と数量の値は数値です。

<u>実際の結果</u>

価格と数量の値は文字列です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](<https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](<https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html>) が含まれる [!DNL Quality Patches Tool] ガイド。
