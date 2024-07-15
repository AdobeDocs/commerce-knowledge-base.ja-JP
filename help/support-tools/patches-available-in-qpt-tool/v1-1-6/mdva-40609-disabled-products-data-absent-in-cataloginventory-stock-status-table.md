---
title: 「MDVA-40609:cataloginventory_stock_status テーブルに無効な製品データがあります」
description: MDVA-40609 パッチを適用すると、無効な製品データが「cataloginventory_stock_status」インデックス テーブルに表示されず、誤った製品数が表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-40609。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 2424c3b3-8bc9-4dd4-908c-9d653f09a57a
feature: Catalog Management, Inventory, Orders, Products
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# MDVA-40609: cataloginventory_stock_status テーブルに無効な製品データがあります

MDVA-40609 パッチを使用すると、`cataloginventory_stock_status` インデックス テーブルに無効な製品データが表示されず、誤った製品数が表示される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.6 がインストールされている場合に使用できます。 パッチ ID は MDVA-40609。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

無効になった製品データは `cataloginventory_stock_status` インデックステーブルに表示されず、誤った製品数量が表示されます。

<u> 前提条件 </u>:

在庫モジュールがインストールされています。

<u> 再現手順 </u>:

1. ストアとストアビューを含む 2 つの web サイトを設定します。
1. 追加のソースと在庫を作成します。
1. シンプルな製品を追加します。
   * 「製品を有効にする」を *いいえ* に設定します。
   * Sourceの項目ステータス =在庫および数量が 0 より大きい 2 つのソースを割り当てます。
1. 商品を保存します。
1. 「**製品の販売可能数量**」タブを確認します。

<u> 期待される結果 </u>:

両方の在庫が 0 より大きい値を入力しました。

<u> 実際の結果 </u>:

1 つの在庫の値がゼロです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
