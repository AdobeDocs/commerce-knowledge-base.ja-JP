---
title: 「ACSD-48661：会社のクレジット制限のコンマ区切り記号の検証の問題」
description: ACSD-48661 パッチを適用すると、Adobe Commerceの問題を修正できます。この問題では、会社のクレジット制限が 999 を超える場合、コンマ区切り記号を使用すると、検証エラーが原因で会社を保存することができません。
exl-id: 85c5a93f-76c5-439b-adcc-511f8473f302
feature: Admin Workspace, B2B, Companies, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# ACSD-48661：会社のクレジット制限のコンマ区切り記号の検証の問題

ACSD-48661 パッチでは、会社のクレジット制限が 999 を超える場合、コンマ区切り記号によって、検証エラーによる会社の保存が妨げられる問題が修正されています。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.26 がインストールされています。 パッチ ID は ACSD-48661 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 - 2.4.5-p1

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社のクレジット制限が 999 を超える場合、コンマ区切り記号を使用すると、検証エラーが原因で会社が保存されるのを防ぐことができます。

<u>再現手順</u>:

1. で会社機能を有効にする **[!UICONTROL Store]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL B2B Features]**.
1. 会社を作成し、の下に 999 を超えるクレジット制限を追加します **[!UICONTROL Company Credit]** タブ。
1. 会社を保存します。
1. 会社を編集して、もう一度保存してみてください。

<u>期待される結果</u>:

クレジット制限を修正せずに会社を保存できます。 金額および価格の入力フィールドでは、コンマはサポートされていません。

<u>実際の結果</u>:

の検証エラーにより、会社を保存できません *[!UICONTROL Credit Limit]* フィールド。 Adobe Commerceでは、次の場合でも、与信限度額に対してコンマ区切り記号が自動的に追加されます [!UICONTROL Credit Limit] フィールドではコンマを使用できません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
