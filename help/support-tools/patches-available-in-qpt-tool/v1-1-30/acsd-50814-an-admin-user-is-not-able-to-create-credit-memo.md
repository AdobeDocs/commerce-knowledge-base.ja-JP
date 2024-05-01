---
title: 「ACSD-50814：管理者ユーザーがクレジットメモを作成できない」
description: 管理者ユーザーがクレジットメモを作成できないAdobe Commerceの問題を修正するには、ACSD-50814 パッチを適用します。
exl-id: bda374cf-6fb7-479f-8130-213ce3cc553e
feature: Admin Workspace, Orders, Returns
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# ACSD-50814：管理者ユーザーがクレジットメモを作成できない

ACSD-50814 パッチは、管理者ユーザーがクレジットメモを作成できない問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.30 がインストールされています。 パッチ ID は ACSD-50814 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーはクレジットメモを作成できません。

<u>再現手順</u>:

1. Adobe Commerce Admin で、に移動します。 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Shipping methods]** > **[!UICONTROL Free shipping]** およびを設定 **[!UICONTROL Enable free shipping]** 対象： *[!UICONTROL Yes]*
1. 再び以下に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Tax]**&#x200B;を開き、計算設定を展開して次を設定します。
   * [!UICONTROL Shipping prices] = [!UICONTROL Including tax]
   * [!UICONTROL Enable cross border trade] = [!UICONTROL No]
1. 価格表示設定を展開し、 [!UICONTROL Display shipping prices] = [!UICONTROL Including tax].
1. を展開 [!UICONTROL Orders], [!UICONTROL Invoices], [!UICONTROL Credit memo] ディスプレイの設定と設定 [!UICONTROL Display shipping amount] = [!UICONTROL Including tax].
1. キャッシュをクリアします。
1. 店頭で注文します。
1. 管理画面で注文の請求書を作成します。
1. クレジットメモを作成します。

<u>期待される結果</u>:

クレジット メモが作成されます。

<u>実際の結果</u>:

次のエラーが発生します。

*エラーにより、ページを表示できません*

```
report.CRITICAL: DivisionByZeroError: Division by zero in vendor/magento/module-sales/Model/Order/Creditmemo/Total/Tax.php:139*
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
