---
title: 「ACSD-54680：複数のソースが割り当てられた製品の B2B 見積もりを処理できない」
description: 複数のソースが割り当てられている商品の B2B Quote が処理できないAdobe Commerceの問題を修正するには、ACSD-54680 パッチを適用します。
feature: B2B
role: Admin, Developer
exl-id: 4d05714c-d32d-46f3-b857-81704c9e96cd
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# ACSD-54680：複数のソースが割り当てられている製品の B2B 見積もりは処理できません。

ACSD-54680 パッチは、複数のソースが割り当てられている製品の B2B Quote が処理できない問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.40 がインストールされています。 パッチ ID は ACSD-54680 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p5

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のソースが割り当てられている製品の B2B 見積もりは処理できません。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Store]** > **[!UICONTROL Sources]** さらに、次の 2 つの新しいソースを作成します。 **ソース 1** および **ソース 2**.
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Store]** > **[!UICONTROL Stocks]** 新しい在庫を作成します。 **在庫 A**&#x200B;を作成し、それをメインの web サイトに割り当てて、 **ソース 1** および **ソース 2** それに。
1. シンプルな製品の作成、割り当て **ソース 1** および **ソース 2**、および Set Qty = *2* 各ソース用。 （商品の販売可能数量は、 *4* その結果）。
1. 会社アカウントを作成します。
1. に移動します **[!UICONTROL Storefront]** そして、会社アカウントにログインします。
1. シンプルな製品を数量=で買い物かごに追加します *4*.
1. を開きます *[!UICONTROL Shopping cart]* をクリックして、 **[!UICONTROL Request a quote]** ボタン。
1. コメントと引用符名を追加して、 **[!UICONTROL Send a Request]** ボタン。
1. に移動 **[!UICONTROL Admin]** > **[!UICONTROL Sales]** > **[!UICONTROL Quotes]**.
1. 最近送信した見積もりを開きます。

<u>期待される結果</u>:

引用された品目には、注文された製品が含まれています。

<u>実際の結果</u>:

引用した項目のページ セクションが空で、引用を処理できません。
`var/log/system.log` 次を含む

```
report.CRITICAL: TypeError: number_format() expects parameter 1 to be float, null given in .../vendor/magento/module-negotiable-quote/Model/QuoteUpdatesInfo.php:232
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
