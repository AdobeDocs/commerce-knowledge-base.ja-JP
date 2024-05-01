---
title: 「ACSD-50234：を使用して注文した場合に、確認メールに記載されている顧客名が正しくない [!DNL PayPal]'
description: を使用して注文するための確認メールで顧客名が正しく表示されないAdobe Commerceの問題を修正するために、ACSD-50234 パッチを適用してください [!DNL PayPal].
exl-id: b2e9c25a-5dd5-4b37-81e3-ca960078da77
feature: Admin Workspace, Communications, Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# ACSD-50234：を使用して注文した場合に、確認メールに記載されている顧客名が正しくない [!DNL PayPal]

ACSD-50234 パッチは、を使用して注文を行ったときに、確認メールに顧客名が正しく表示されない問題を修正します [!DNL PayPal]. このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.29 がインストールされています。 パッチ ID は ACSD-50234 です。 この問題はAdobe Commerce 2.4.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.7 ～ 2.4.4-p3

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

を使用して行われた注文の確認メール [!DNL PayPal] に間違った顧客名が表示される。

<u>再現手順</u>

1. Enable （有効） **[!UICONTROL PayPal Express Checkout]**.
1. ゲストとしてフロントエンドに移動します。
1. 商品を買い物かごに追加します。
1. チェックアウト方法 **[!UICONTROL PayPal Express Checkout]** 支払方法として。
1. 注文確認メールを確認します。

<u>期待される結果</u>

注文確認メール、請求書メール、およびすべての出荷関連メールは、顧客名を宛先としています。

<u>実際の結果</u>

注文確認メール、請求書メールおよびすべての出荷関連メールの宛先は次のとおりです *ゲスト*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
