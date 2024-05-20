---
title: 「MDVA-40609:cataloginventory_stock_status テーブルに無効な製品データがあります」
description: MDVA-40609 パッチを適用すると、無効な製品データが「cataloginventory_stock_status」インデックス テーブルに表示されず、誤った製品数が表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-40609。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 2424c3b3-8bc9-4dd4-908c-9d653f09a57a
feature: Catalog Management, Inventory, Orders, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# MDVA-40609: cataloginventory_stock_status テーブルに無効な製品データがあります

MDVA-40609 パッチを適用すると、無効にされた製品データがに表示されない問題が解決されます `cataloginventory_stock_status` 誤った製品数量が表示されるインデックステーブル。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.6 がインストールされています。 パッチ ID は MDVA-40609。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

無効になった製品データはに表示されません `cataloginventory_stock_status` 誤った製品数量が表示されるインデックステーブル。

<u>前提条件</u>:

在庫モジュールがインストールされています。

<u>再現手順</u>:

1. ストアとストアビューを含む 2 つの web サイトを設定します。
1. 追加のソースと在庫を作成します。
1. シンプルな製品を追加します。
   * 「製品を有効にする」を次のように設定 *不可*.
   * ソース品目ステータス = Instock および数量が 0 より大きい 2 つのソースを割り当てます。
1. 商品を保存します。
1. を確認します **商品販売可能数量** タブ。

<u>期待される結果</u>:

両方の在庫が 0 より大きい値を入力しました。

<u>実際の結果</u>:

1 つの在庫の値がゼロです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
