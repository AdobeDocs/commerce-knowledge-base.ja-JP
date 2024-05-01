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

ACSD-49179 パッチは、異なる店舗で異なる通貨が使用されている場合に、注文レポートに誤った金額が表示される問題を修正します。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.28 がインストールされています。 パッチ ID は ACSD-49179 です。 この問題はAdobe Commerce 2.4.7 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.6

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

注文レポートには、店舗ごとに異なる通貨の場合に誤った金額が表示されます。

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Config]** > **[!UICONTROL Catalog]** > **[!UICONTROL Price]** およびを設定 [!UICONTROL Catalog Price Scope] = [!UICONTROL Website].
1. 追加の web サイト、ストア、ストア表示を作成します。
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Config]** > **[!UICONTROL General]** > **[!UICONTROL Currency Setup]** > **[!UICONTROL Currency Options]** さらに、次のように設定します。
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
1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Currency]** > **[!UICONTROL Currency Rates]** そして、THB の空のコンバージョン率を設定します（レートを 1.0000 に設定）。
1. 製品を作成して両方の web サイトに割り当て、以前に作成した追加の web サイトでこの製品を注文します。
1. 注文が行われていることを確認します。 *処理* ステータス （請求書）。
1. バックエンドで、に移動します。 **[!UICONTROL Reports]** > **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. 「」をクリック **[!UICONTROL Yellow]** 統計の更新を警告しています。
1. 作成済みの追加 web サイトでレポートの範囲を設定し、次のようにフィルターを設定します。
   * [!UICONTROL Date Used]: [!UICONTROL Created]
   * [!UICONTROL Period]: [!UICONTROL Day]
   * [!UICONTROL From and To]：テストオーダーを行った同じ日
   * [!UICONTROL Order Status]: [!UICONTROL Any]
   * [!UICONTROL Empty rows]: [!UICONTROL No]
   * [!UICONTROL Show Actual Values]: [!UICONTROL No]

<u>期待される結果</u>:

売上高の合計は、Web サイトの通貨に変換された正しい金額を示します。

<u>実際の結果</u>:

合計はゼロです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
