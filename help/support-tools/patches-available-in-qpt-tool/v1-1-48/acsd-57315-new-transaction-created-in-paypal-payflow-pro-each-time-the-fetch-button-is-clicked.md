---
title: '''ACSD-57315：新しいトランザクションがで作成されます [!DNL PayPal Payflow Pro] 「取得」ボタンをクリックするたびに'
description: ACSD-57315 パッチを適用して、で新しいトランザクションが作成されるAdobe Commerceの問題を修正してください。 [!DNL PayPal Payflow Pro] の「トランザクションを表示」画面で「取得」ボタンをクリックするたびに [!UICONTROL Admin].
feature: Payments
role: Admin, Developer
exl-id: bcc7467d-09f9-4235-9f9f-46d3034567b8
source-git-commit: d7ace1f20defb01105d4a241f971b06fca052215
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# ACSD-57315：新しいトランザクションがで作成されます [!DNL PayPal Payflow Pro] 「取得」ボタンをクリックするたびに、

ACSD-57315 パッチは、で新しいトランザクションが作成される問題を修正します。 [!DNL PayPal Payflow Pro] の「トランザクションを表示」画面で「取得」ボタンをクリックするたびに [!UICONTROL Admin]. このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.48 がインストールされています。 パッチ ID は ACSD-57315 です。 この問題はAdobe Commerce 2.5.0 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

新しいトランザクションがで作成されます。 [!DNL PayPal Payflow Pro] の「トランザクションを表示」画面で「取得」ボタンをクリックするたびに [!UICONTROL Admin].

<u>再現手順</u>:

1. 設定 [!DNL PayPal Payflow Pro].
1. トランザクションメソッドをに設定します *[!UICONTROL Sale]*.
1. を使用した注文 *クレジットカード*.
1. トランザクションを次から開きます [!UICONTROL Admin].
1. 「」をクリック **[!UICONTROL Fetch]** ボタン。
1. チェック [!DNL PayPal] 注文に関連するトランザクションの勘定。

<u>期待される結果</u>:

新しい支払トランザクションは作成されません。

<u>実際の結果</u>:

既に支払いが行われた注文に対して、新しい支払いトランザクションが作成されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
