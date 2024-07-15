---
title: 「MDVA-28202 パッチ：在庫切れ製品が適切にフィルタリングされない」
description: MDVA-28202 パッチは、Adobe Commerce ストアのフロントエンドで**価格** フィルターを使用して、在庫切れの商品が適切にフィルタリングされない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） v.1.0.6 がインストールされている場合に利用できます。
exl-id: 45976602-15f3-4fef-9d90-da2b3fe6046d
feature: Catalog Management, Categories, Orders, Products
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# MDVA-28202 パッチ：在庫切れの製品が適切にフィルタリングされない

MDVA-28202 パッチは、在庫切れの商品がAdobe Commerce ストアのフロントエンドで **価格** フィルターを使用して適切にフィルタリングされない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) v.1.0.6 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャー 2.3.5-p1 上のAdobe Commerce用に設計されました。
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.4 ～ 2.4.1 とも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

在庫切れ商品が、Commerce管理の **価格** フィルターを使用して適切にフィルタリングされない。

<u> 前提条件：</u>

* **ストア/設定/カタログ/在庫/在庫オプション** で、*在庫切れ商品を表示&#x200B;**=「* はい**」を設定します。

<u> 再現手順：</u>

1. 2 つのシンプルな製品を使用して設定可能な製品を作成します（例：set **Price** = *$1500*）。
1. 設定可能な製品を作成する際は、単純な製品はどちらも「在庫切れ」になっている必要があります。
1. この設定可能な製品をカテゴリに割り当てます。
1. 上記の設定可能な商品 `catalog_product_index_price` エンティティ ID を使用して、テーブルのインデックスを再作成して確認します。
1. すべての製品価格= *$0* を保存します。
1. カテゴリを読み込んで、商品の可用性を確認します。
1. レイヤーナビゲーションから **価格** フィルターを開きます。
1. **価格** フィルターのオプションは「*$0.00 - 9.99*」であることに注意してください。
1. 上記の **価格** フィルターオプションをクリックして、**価格** = *$1500* を設定すると、上記で作成した設定可能な製品が取得されます。

<u> 期待される結果：</u>

製品は、期待どおりに正しい価格範囲でフィルタリングされます。

<u> 実際の結果：</u>

製品が間違った価格範囲フィルターに該当します。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Quality Patches Tool を使用したパッチの適用 ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)。
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。

設定可能な製品について詳しくは、開発者向けドキュメントの次の記事を参照してください。[ 設定可能な製品の作成 ](https://devdocs.magento.com/guides/v2.4/rest/tutorials/configurable-product/config-product-intro.html) チュートリアルについては、開発者向けドキュメントを参照してください。
