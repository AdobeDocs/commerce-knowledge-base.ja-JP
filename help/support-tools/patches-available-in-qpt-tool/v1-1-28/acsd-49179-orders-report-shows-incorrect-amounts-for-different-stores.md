---
title: 「ACSD-49179：注文レポートに、異なる店舗に対して誤った金額が表示される。」
description: ACSD-49179 パッチを適用すると、店舗ごとに異なる通貨が使用されている場合に注文レポートに誤った金額が表示されるAdobe Commerceの問題を修正できます。
exl-id: 01e4cd2d-6c33-4cf5-bf31-bbc34eaaed1a
feature: Admin Workspace, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# ACSD-49179：注文レポートに、様々な店舗に対して誤った金額が表示される

ACSD-49179 パッチは、異なる店舗で異なる通貨が使用されている場合に、注文レポートに誤った金額が表示される問題を修正します。 このパッチは、[[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされている場合に使用できます。 パッチ ID は ACSD-49179 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文レポートには、店舗ごとに異なる通貨の場合に誤った金額が表示されます。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Config]**/**[!UICONTROL Catalog]**/**[!UICONTROL Price]** に移動し、[!UICONTROL Catalog Price Scope]=[!UICONTROL Website] を設定します。
1. 追加の web サイト、ストア、ストア表示を作成します。
1. **[!UICONTROL Stores]**/**[!UICONTROL Config]**/**[!UICONTROL General]**/**[!UICONTROL Currency Setup]**/**[!UICONTROL Currency Options]** に移動し、次のように設定します。
   * デフォルトの設定：
      * 基準通貨：USD
      * 既定の表示通貨：USD
      * 使用可能な通貨：EUR、USD および THB （タイバーツ）
   * メインウェブサイト：
      * 基準通貨：EUR
      * デフォルト表示通貨：EUR
      * 使用可能な通貨：EUR
   * 追加の新しい Web サイト：
      * 基準通貨：THB （タイバーツ）
      * 既定の表示通貨：THB （タイ バーツ）
      * 使用可能な通貨：THB （タイバーツ）
1. **[!UICONTROL Stores]**/**[!UICONTROL Currency]**/**[!UICONTROL Currency Rates]** に移動して、THB の空のコンバージョン率を設定します（率を 1.0000 に設定します）。
1. 製品を作成して両方の web サイトに割り当て、以前に作成した追加の web サイトでこの製品を注文します。
1. 注文が *処理中* ステータスであることを確認します（請求書）。
1. バックエンドで、**[!UICONTROL Reports]** / **[!UICONTROL Sales]** / **[!UICONTROL Orders]** に移動します。
1. 統計を更新するには、**[!UICONTROL Yellow]** の警告をクリックします。
1. 作成済みの追加 web サイトでレポートの範囲を設定し、次のようにフィルターを設定します。
   * [!UICONTROL Date Used]: [!UICONTROL Created]
   * [!UICONTROL Period]: [!UICONTROL Day]
   * [!UICONTROL From and To]: テスト注文を行った同じ日
   * [!UICONTROL Order Status]: [!UICONTROL Any]
   * [!UICONTROL Empty rows]: [!UICONTROL No]
   * [!UICONTROL Show Actual Values]: [!UICONTROL No]

<u> 期待される結果 </u>:

売上高の合計は、Web サイトの通貨に変換された正しい金額を示します。

<u> 実際の結果 </u>:

合計はゼロです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
