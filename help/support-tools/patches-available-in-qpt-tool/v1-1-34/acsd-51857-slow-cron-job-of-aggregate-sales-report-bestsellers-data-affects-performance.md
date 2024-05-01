---
title: 「ACSD-51857:「aggregate_sales_report_bestsellers_data」の低速 cron ジョブがパフォーマンスに影響を与える」
description: ACSD-51857 パッチを適用すると、cron ジョブ「aggregate_sales_report_bestsellers_data」が大きな「sales_order」および「sales_order_item」データベーステーブルに影響を与えるAdobe Commerceの問題が修正されます。
exl-id: 444ab283-c98b-46b3-a492-706f0ce34a27
source-git-commit: a33364531d2efd572cd1b1847dd45e0f427af03b
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# ACSD-51857：の cron ジョブが遅い `aggregate_sales_report_bestsellers_data` パフォーマンスに影響する

ACSD-51857 パッチは、cron ジョブが遅い問題を修正します `aggregate_sales_report_bestsellers_data` 大きな影響を与える `sales_order` および `sales_order_item` データベーステーブル。 このパッチは、 [[!DNL Quality Patches Tool (QPT)]](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.34 がインストールされています。 パッチ ID は ACSD-51857 です。 この問題はAdobe Commerce 2.4.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.6-p2

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

の Cron ジョブパフォーマンス `aggregate_sales_report_bestsellers_data` が遅い `sales_order` および `sales_order_item` データベーステーブル。

これを解決するために、レポートのデータを取得するメインのデータクエリを、より効率的なフォームに書き直しました。 サブクエリを使用してデータのサブセットを決定するようになりました。

サブクエリをできるだけ早く機能させるために、に新しいインデックスを追加しました `sales_order` データベース テーブル： `SALES_ORDER_STORE_STATE_CREATED` 基準： `store_id`, `state`、および `created_at` 列。

<u>前提条件</u>

毎日多数の注文を確認してください。

<u>再現手順</u>

1. を実行 `aggregate_sales_report_bestsellers_data` cron ジョブ。
1. 管理ダッシュボードの下に表示するデータを **[!UICONTROL Bestsellers]** タブ。

<u>期待される結果</u>:

*[!UICONTROL Quantity per source]* の下 **[!UICONTROL Configuration]** タブは空にしないでください。

<u>実際の結果</u>:

*[!UICONTROL Quantity per source]* の下 **[!UICONTROL Configuration]** タブが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
