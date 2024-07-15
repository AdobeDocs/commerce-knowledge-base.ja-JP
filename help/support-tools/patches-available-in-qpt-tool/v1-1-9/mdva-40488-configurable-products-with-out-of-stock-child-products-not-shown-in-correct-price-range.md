---
title: 「MDVA-40488：在庫切れの子製品が正しい価格範囲で表示されない設定可能な製品」
description: MDVA-40488 パッチを使用すると、在庫切れの子製品を含む設定可能な製品が正しい価格範囲で表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-40488。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 0c4b9f5e-ae41-409e-b244-1d7cf948ed6f
feature: Configuration, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# MDVA-40488：在庫切れの子製品が正しい価格範囲で表示されない設定可能な製品

MDVA-40488 パッチを使用すると、在庫切れの子製品を含む設定可能な製品が正しい価格範囲で表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.9 がインストールされている場合に使用できます。 パッチ ID は MDVA-40488。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの子製品を含む設定可能な製品が、正しい価格範囲で表示されない。

<u> 前提条件 </u>:

Commerce管理者/**stores**/**configuration**/**catalog**/**Inventory**/**Stock options** に移動し、「**在庫切れ商品を表示**」設定を「*はい*」に設定します。

<u> 再現手順 </u>:

1. 2 つの関連する製品を使用して設定可能な製品を作成します。 例：単純な製品赤と茶色。
1. シンプルな商品の在庫を赤に設定し、在庫ステータスを *在庫中* に設定してから、商品の有効ステータスを *いいえ* に設定します。
1. 単純製品の在庫を「ブラウン」に設定し、「製品の有効化」ステータスを *Yes* に設定します。
1. 設定可能な製品の在庫ステータスが *在庫中* であることを確認します。
1. シンプル商品の在庫を Brown から 0 に変更し、在庫ステータスを *在庫切れ* に設定します。
1. この時点では、設定可能な商品の在庫ステータスは *在庫* のままです。
1. 再インデックスを実行します。
1. `catalog_product_index_price` DB テーブル内の設定可能な製品の `min_price` と `max_price` をチェックします。2 つの値は 0 に設定されています。
1. ただし、設定可能な商品の在庫ステータスを *在庫切れ* に設定してインデックス再作成を行うと、設定可能な商品のゼロ以外の `min_price` と `max_price` の値を確認できます。

<u> 期待される結果 </u>:

子製品がすべて *在庫切れ* で、設定可能な製品自体も *在庫切れ* の場合、価格はすべての子製品を使用して計算されます。

<u> 実際の結果 </u>:

`catalog_product_index_price` DB テーブルの設定可能なプロダクトの `min_price` と `max_price` の値は、設定可能なストックステータスが *在庫切れ* の場合は 0 に設定されますが、在庫切れ *の場合は* 0 以外の値になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
