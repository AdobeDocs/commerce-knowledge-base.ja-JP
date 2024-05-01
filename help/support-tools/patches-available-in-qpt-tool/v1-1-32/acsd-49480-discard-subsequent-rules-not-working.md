---
title: 「ACSD-49480：機能しない後続のルールを破棄する」
description: Adobe Commerce ACSD-49480 パッチを適用して、 [!UICONTROL Cart Price Rule - Discard Subsequent Rules] は意図したとおりに動作していません。
exl-id: 8d306a9e-ed1a-4295-8130-81700cbf31a6
feature: Price Rules
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# ACSD-49480: [!UICONTROL Cart Price Rule - Discard Subsequent Rules] は意図したとおりに動作していません

ACSD-49480 パッチは、 [!UICONTROL Cart Price Rule - Discard Subsequent Rules] は意図したとおりに動作していません。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.32 がインストールされています。 パッチ ID は ACSD-49480 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

[!UICONTROL Cart Price Rule - Discard Subsequent Rules] は意図したとおりに動作していません。

<u>再現手順</u>:

1. を作成 **[!UICONTROL Cart Price Rule]** クーポンコードを使用（という名前 *テスト*）に 10 ドルの割引が適用されます。 *製品 ID 1* が含まれる **[!UICONTROL Actions]** tab キー [!UICONTROL Discard Subsequent Rules] をに設定 *[!UICONTROL Yes]* および [!UICONTROL Priority] をに設定 *1*.
1. 別のを作成 **[!UICONTROL Cart Price Rule]** に 5 ドル割引のクーポンコードが付いていない *製品 ID 2* が含まれる **[!UICONTROL Actions]** tab キー [!UICONTROL Priority] をに設定 *2*. ここでは、これがグローバル販売であると仮定します。 *製品 ID 2*.
1. フロントエンドサイトに移動して、を追加します *製品 ID 1* および *製品 ID 2* カートに入れます。
1. を適用 *テスト* クーポンコード。

<u>期待される結果</u>

* *割引 1* 適用先 *製品 ID 1*.
* *割引 2* 適用先 *製品 ID 2*.

<u>実際の結果</u>

* のみ *割引 1* 適用先 *製品 ID 1*.
* *割引 2* はに適用されません *製品 ID 2*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
