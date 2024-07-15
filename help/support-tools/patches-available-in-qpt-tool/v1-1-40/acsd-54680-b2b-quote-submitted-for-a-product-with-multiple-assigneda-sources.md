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

ACSD-54680 パッチは、複数のソースが割り当てられている製品の B2B Quote が処理できない問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.40 がインストールされている場合に使用できます。 パッチ ID は ACSD-54680 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5-p5

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のソースが割り当てられている製品の B2B 見積もりは処理できません。

<u> 再現手順 </u>:

1. **[!UICONTROL Admin]**/**[!UICONTROL Store]**/**[!UICONTROL Sources]** に移動して、2 つの新しいソース（**Source 1** と **Source 2** を作成します。
1. **[!UICONTROL Admin]**/**[!UICONTROL Store]**/**[!UICONTROL Stocks]** に移動して、新しい在庫を作成します。**在庫 A** をメイン web サイトに割り当て、**Source 1** と **Source 2** を割り当てます。
1. シンプルな商品を作成し、**Source 1} と** 2}Source 2 **を割り当て、各ソースに対して数量= *2* を設定します。**（その結果、製品の販売可能数量は *4* になります。）
1. 会社アカウントを作成します。
1. **[!UICONTROL Storefront]** に移動し、会社アカウントにログインします。
1. シンプルな製品を数量= *4* で買い物かごに追加します。
1. *[!UICONTROL Shopping cart]* を開いて「」ボタン **[!UICONTROL Request a quote]** クリックします。
1. コメントと引用符名を追加し、「」ボタン **[!UICONTROL Send a Request]** クリックします。
1. **[!UICONTROL Admin]**/**[!UICONTROL Sales]**/**[!UICONTROL Quotes]** に移動します。
1. 最近送信した見積もりを開きます。

<u> 期待される結果 </u>:

引用された品目には、注文された製品が含まれています。

<u> 実際の結果 </u>:

引用した項目のページ セクションが空で、引用を処理できません。
`var/log/system.log` contains

```
report.CRITICAL: TypeError: number_format() expects parameter 1 to be float, null given in .../vendor/magento/module-negotiable-quote/Model/QuoteUpdatesInfo.php:232
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
