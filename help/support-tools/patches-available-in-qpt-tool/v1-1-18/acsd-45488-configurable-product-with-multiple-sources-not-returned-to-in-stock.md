---
title: 「ACSD-45488：複数のソースを持つ設定可能な製品で、在庫に自動的に戻されない」
description: ACSD-45488 パッチを使用すると、複数のソースを持つ設定可能な製品が在庫として自動的に返されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.18 がインストールされている場合に利用できます。 パッチ ID は ACSD-45488 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 83332226-b14e-4d36-bf65-170f55fff270
feature: Configuration, Orders, Products, Returns
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# ACSD-45488：複数のソースを持ち、在庫に自動的に戻されない設定可能な製品

ACSD-45488 パッチを使用すると、複数のソースを持つ設定可能な製品が在庫として自動的に返されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.18 がインストールされている場合に使用できます。 パッチ ID は ACSD-45488 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数のソースを持つ設定可能な製品は、在庫に自動的には戻されません。

<u> 再現手順 </u>:

1. サブ在庫ソースを作成します。
1. 関連する 2 つの仮想製品を使用して設定可能な製品を作成します。
1. 関連製品をデフォルトの在庫ソースに割り当て、数量を 1 に設定します。
1. `cataloginventory_stock_status` から `stock_status` を確認します。
1. 関連する両方の製品を *在庫切れ* に設定します。
1. `cataloginventory_stock_status` から `stock_status` を確認します。
1. 関連する両方の製品を *在庫* に設定します。
1. `cataloginventory_stock_status` から `stock_status` を確認します。

<u> 期待される結果 </u>:

関連する商品が在庫中に設定されると、設定可能な商品の在庫ステータスが *在庫中* に更新されます。

<u> 実際の結果 </u>:

関連する商品が在庫中に設定されている場合、設定可能な商品の在庫ステータスは *在庫中* に更新されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
