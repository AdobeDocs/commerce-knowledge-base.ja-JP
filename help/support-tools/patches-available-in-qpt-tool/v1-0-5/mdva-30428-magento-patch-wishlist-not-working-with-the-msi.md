---
title: 「MDVA-30428：ウィッシュリストがInventory managementで機能しない」
description: MDVA-30428 パッチは、Inventory management（MSI）で動作しないウィッシュリストを解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。
exl-id: 79e8d5d6-b073-48cf-8ecc-5c44667c12ad
feature: Inventory, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# MDVA-30428：ウィッシュリストがInventory managementで機能しない

MDVA-30428 パッチは、Inventory management（MSI）で動作しないウィッシュリストを解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.5 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3 ～ 2.3.3-p1 （QPT 1.0.6）および 2.3.5 ～ 2.4.1 （QPT 1.0.5）

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ウィッシュリストに製品を追加すると、その製品がカスタムインベントリソースに割り当てられたときに、次のメッセージが表示されます」*現在、ウィッシュリストに商品を追加できません：在庫のない商品をウィッシュリストに追加することはできません。*“

<u>再現手順</u>:

1. Commerce Admin で新しいインベントリソースを作成します。 手順については、次を参照してください [カタログ /新しいソースの追加](https://docs.magento.com/user-guide/catalog/inventory-sources-add.html?itm_source=merchdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=new%20inventory%20source) を参照してください。
1. Commerce管理者で新しい在庫を作成し、新しいソースおよびデフォルトの web サイトを新しい在庫に割り当てます。 手順については、次を参照してください [カタログ /新しい在庫の追加](https://docs.magento.com/user-guide/catalog/inventory-stock-add.html#add-new-stock) を参照してください。
1. シンプルな商品を作成し、新しい在庫を在庫として割り当てます。
1. フロントエンドのシンプルな製品詳細ページにアクセスします。
1. 商品をウィッシュリストに追加します。 次のエラーが表示されます。 *現在、ウィッシュリストにアイテムを追加できません：在庫のない商品をウィッシュリストに追加することはできません*.

<u>期待される結果</u>:

商品は、カスタムストックと共にウィッシュリストに追加される必要があります。

<u>実際の結果</u>:

商品がウィッシュリストに追加されず、エラーメッセージが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
