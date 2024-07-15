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

MDVA-33281 パッチは、インベントリの 3 つの不整合の問題を修正します。 「イシュー」セクションでリンクされているイシューをクリックして、これらのエラーを再現する手順を確認します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.14 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.4 - 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

このパッチは、次のようなインベントリの不整合の問題を修正します。

* **PHP 致命的エラー** SKU パラメータータイプが正しくな `bin/magento inventory:reservation:list-inconsistencies` ため、CLI で PHP を実行すると発生します。
* 不整合リストの **重複データ**。
* **新規予約** は、注文前（注文後の予約に基づく事前適合）に作成されます。 ご注文の際にエラーが発生した場合は、ご注文に応じて追加の予約を行います。

>[!NOTE]
>
>また、`inventory_reservation` テーブルに、開発者向けドキュメントで予期せず多数の [ 予約の不整合 ](https://devdocs.magento.com/guides/v2.4/inventory/inventory-cli-reference.html#what-causes-reservation-inconsistencies) が発生する問題を解決するパッチ MDVA-30112 もあります。 この解決策については、サポート サポート サポート ナレッジ ベースの「[MDVA-30112 Magento パッチ：大量の予約の不整合 ](/help/support-tools/patches-available-in-qpt-tool/v1-0-8/mdva-30112-magento-patch-large-number-reservation-inconsistencies.md)」を参照してください。

## PHP 致命的エラー

<u> 再現手順 </u>:

PHP `bin/magento inventory:reservation:list-inconsistencies` の実行中に致命的なエラーが発生する。

予約の不整合の一覧を取得するには、本番サーバにログインし、CLI で次のコマンドを実行します（– r switch - raw 出力）。

<pre>bin/magento inventory:reservation:list-inconsistencies -r</pre>

<u> 期待される結果 </u>:

予約の不整合のリストが作成されます。 これらは、次の形式で返されます

```plaintext
<ORDER_INCREMENT_ID>:<SKU>:<QUANTITY>:<STOCK-ID>
```

<u> 実際の結果 </u>:

PHP Fatal Error が出力される。

## データを複製

重複データは `inventory_reservation table` にあります。

<u> 再現手順 </u>:

予約の不整合のトラブルシューティングを行うには、次のコマンドを実行します。

<pre>SELECT *, COUNT （*）
FROM inventory_reservation
メタデータ、SKU、数量でグループ化
COUNT （*） &gt; 1 である</pre>

<u> 期待される結果 </u>:

重複はありません。

<u> 実際の結果 </u>:

重複があります。

## 新規予約

<u> 再現手順 </u>:

注文前に作成された新しい予約：

1. データベースを読み込みます。
1. ターミナルで `bin/magento setup:upgrade` を実行します。
1. ターミナルで `bin/magento inventory:reservation:list-inconsistencies        -i -r` を実行して、不整合をリストします。

<u> 期待される結果 </u>:

ループが発生せず、迅速に結果が得られます。

<u> 実際の結果 </u>:

システム設定に応じて、無限ループで同じ結果が表示されるか、コマンドが `memory_limit` で失敗します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
