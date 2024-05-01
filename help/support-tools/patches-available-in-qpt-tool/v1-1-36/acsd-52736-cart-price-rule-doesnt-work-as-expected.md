---
title: '"ACSD-52736: [!UICONTROL Cart Price Rule] が期待どおりに動作しません」'
description: を使用してAdobe Commerceの問題を修正するために ACSD-52736 パッチを適用します。 [!UICONTROL Cart Price Rule] 設定可能な製品数量の要件が含まれていますが、期待どおりに動作しません。
feature: Shopping Cart, Products
role: Admin, Developer
exl-id: 8403b418-b197-4695-88a8-e322b18cd4ad
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# ACSD-52736: [!UICONTROL Cart Price Rule] が期待どおりに動作しない

ACSD-52736 パッチは、 [!UICONTROL Cart Price Rule] 設定可能な製品数量の要件が含まれていますが、期待どおりに動作しません。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.36 がインストールされています。 パッチ ID は ACSD-52736 です。 この問題はAdobe Commerce 2.4.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

A [!UICONTROL Cart Price Rule] これには設定可能な製品数量の要件が含まれていますが、期待どおりに動作しません。

<u>再現手順</u>:

1. 買い物かごルールを作成します。
   * [!UICONTROL Apply] =製品価格割引率
   * [!UICONTROL Discount Amount] = 60
   * [!UICONTROL Maximum Qty Discount is Applied to] = 1
   * [!UICONTROL Discount Qty Step (Buy X)] = 1
   * 次の条件に一致する買い物かご品目にのみルールを適用します：買い物かごの数量は 1 です
2. を使用した製品の追加 [!UICONTROL Qty] = 2、買い物かごに追加されます。
3. 買い物かごの価格を確認します。

<u>期待される結果</u>:

カート内の商品の数量がであるため、ルールは適用されません *2*.

<u>実際の結果</u>:

割引が適用されます。

<u> パッチのインストール後に必要な追加手順</u>:

パッチを適用した後、を使用して買い物かごルールの条件 *数量* 属性を削除してから再度追加する必要があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
