---
title: 「MDVA-33281 パッチ：インベントリの不整合の問題」
description: MDVA-33281 パッチは、インベントリの 3 つの不整合の問題を修正します。 「イシュー」セクションでリンクされているイシューをクリックして、これらのエラーを再現する手順を確認します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.14 がインストールされている場合に利用できます。
exl-id: adba9728-6e42-467e-943d-cf8af0bec353
feature: Inventory, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# MDVA-33281 パッチ：インベントリ不整合の問題

MDVA-33281 パッチは、インベントリの 3 つの不整合の問題を修正します。 「イシュー」セクションでリンクされているイシューをクリックして、これらのエラーを再現する手順を確認します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.14 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.4 - 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

このパッチは、次のようなインベントリの不整合の問題を修正します。

* **PHP 致命的エラー** 実行中 `bin/magento inventory:reservation:list-inconsistencies` SKU パラメータータイプが正しくないため、CLI で調整する。
* **データを複製** 矛盾リスト内。
* **新規予約** 注文の前に作成されます（注文後の予約に基づく以前の適合）。 ご注文の際にエラーが発生した場合は、ご注文に応じて追加の予約を行います。

>[!NOTE]
>
>また、MDVA-30112 というパッチもあり、このパッチを使用すると、の数が予想外に多くなる問題を解決できます。 [予約の不整合](https://devdocs.magento.com/guides/v2.4/inventory/inventory-cli-reference.html#what-causes-reservation-inconsistencies) 開発者向けドキュメント、 `inventory_reservation` テーブル。 解決策については、次を参照してください： [MDVA-30112 Magento パッチ：大量のリザベーションの不整合](/help/support-tools/patches-available-in-qpt-tool/v1-0-8/mdva-30112-magento-patch-large-number-reservation-inconsistencies.md) サポートナレッジベースで。

## PHP 致命的エラー

<u>再現手順</u>:

実行中に PHP 致命的エラーが発生する `bin/magento inventory:reservation:list-inconsistencies`.

予約の不整合の一覧を取得するには、本番サーバにログインし、CLI で次のコマンドを実行します（– r switch - raw 出力）。

<pre>bin/magento インベントリ:reservation:list-inconsistencies -r</pre>

<u>期待される結果</u>:

予約の不整合のリストが作成されます。 これらは、次の形式で返されます

```plaintext
<ORDER_INCREMENT_ID>:<SKU>:<QUANTITY>:<STOCK-ID>
```

<u>実際の結果</u>:

PHP Fatal Error が出力される。

## データを複製

重複データはにあります `inventory_reservation table`.

<u>再現手順</u>:

予約の不整合のトラブルシューティングを行うには、次のコマンドを実行します。

<pre>COUNT （*） &gt; 1 のメタデータ、SKU、数量で INVENTORY_RESERVATION グループから*、COUNT （*）を選択します</pre>

<u>期待される結果</u>:

重複はありません。

<u>実際の結果</u>:

重複があります。

## 新規予約

<u>再現手順</u>:

注文前に作成された新しい予約：

1. データベースを読み込みます。
1. 実行 `bin/magento setup:upgrade` ターミナルの中です。
1. 次を実行して不整合をリスト `bin/magento inventory:reservation:list-inconsistencies        -i -r` ターミナルの中です。

<u>期待される結果</u>:

ループが発生せず、迅速に結果が得られます。

<u>実際の結果</u>:

同様の結果が無限ループに表示されるか、コマンドが次のエラーで失敗します `memory_limit`（システム設定に応じて異なります）。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
