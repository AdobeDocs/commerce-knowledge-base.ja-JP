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

MDVA-40488 パッチを使用すると、在庫切れの子製品を含む設定可能な製品が正しい価格範囲で表示されない問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.9 がインストールされています。 パッチ ID は MDVA-40488。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れの子製品を含む設定可能な製品が、正しい価格範囲で表示されない。

<u>前提条件</u>:

Commerce管理者に移動します **ストア** > **設定** > **カタログ** > **在庫** > **在庫オプション** およびを設定 **在庫切れ商品の表示** 設定： *はい*.

<u>再現手順</u>:

1. 2 つの関連する製品を使用して設定可能な製品を作成します。 例：単純な製品赤と茶色。
1. 単純商品の在庫を赤に設定し、在庫ステータスをに設定します *在庫あり*&#x200B;を選択してから、「製品を有効にする」ステータスをに設定します。 *不可*.
1. シンプル製品の在庫をブラウンに設定してから、製品の有効化ステータスを次のように設定します *はい*.
1. 設定可能な製品の在庫ステータスがであることを確認します。 *在庫あり*.
1. シンプル製品 Brown の在庫を 0 に変更し、在庫状態をに設定します。 *在庫切れ*.
1. この時点では、設定可能な商品の在庫ステータスは、引き続きになります *在庫あり*.
1. 再インデックスを実行します。
1. を確認します `min_price` および `max_price` の設定可能な製品について `catalog_product_index_price` DB テーブル - 2 つの値は 0 に設定されます。
1. ただし、設定可能な製品の在庫ステータスをに設定した場合は、 *在庫切れ* そして、再インデックスを実行すると、ゼロ以外の値が表示されます `min_price` および `max_price` 設定可能な商品の値。

<u>期待される結果</u>:

すべての子製品が *在庫切れ* 設定可能な製品自体も次の通りです *在庫切れ*&#x200B;は、すべての子製品を使用して価格が計算されます。

<u>実際の結果</u>:

この `min_price` および `max_price` の設定可能な商品の値 `catalog_product_index_price` 設定可能な在庫ステータスがの場合、DB テーブルは 0 に設定されます。 *在庫あり*&#x200B;しかし、もしそうなら *在庫切れ* これらの値はゼロ以外の値になります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
