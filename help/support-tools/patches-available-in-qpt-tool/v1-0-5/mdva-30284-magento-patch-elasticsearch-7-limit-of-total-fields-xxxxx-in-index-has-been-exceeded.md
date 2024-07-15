---
title: 「MDVA-30284 パッチ：Elasticsearch7 - インデックスの合計フィールド数の制限 [XXXXX] を超えています」
description: MDVA-30284 パッチを適用すると、Elasticsearch 7 を使用したときに「インデックスの合計フィールド数の制限\[XXXXX\] を超えています」というエラーメッセージが表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） v.1.0.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-30284。
exl-id: cf840558-891a-4a7e-8900-b8434f703be0
feature: Search, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# MDVA-30284 パッチ：Elasticsearch7 - インデックスの合計フィールド数 [XXXXX] の制限を超えています

MDVA-30284 パッチを適用すると、Elasticsearch 7 を使用したときに「インデックスの合計フィールド数の制限\[XXXXX\] を超えています」というエラーメッセージが表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.5 がインストールされている場合に使用できます。 パッチ ID は MDVA-30284。

## 影響を受ける製品とバージョン

* このパッチは、Cloud Infrastructure 2.3.5-p2 上のAdobe Commerce用に設計されました
* Elasticsearch 7 はAdobe Commerce 2.3.5 および 2.4.x と互換性があります

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Elasticsearchフィールドの制限が正しくないため、\[catalogsearch\_fulltext\] インデクサーを実行すると次のエラーが発生します：

*インデックス [xxxxxx] の合計フィールド [xxx] の制限を超えています*

この問題は、多数の製品属性がある場合に発生します。 この問題は、Elasticsearchがフィールド数を計算する方法によってトリガーされます。 フィールドが割り当てられている属性がある場合、これらのフィールドは個別のインデクサーとしてインデックスを作成することがあります。 その結果、上限を超える警告が発生します。

<u> 再現手順：</u>

<u> 前提条件 </u>

* module-elasticsearch 100.3.5 をインストール。
* Elasticsearch 7 がインストールされました。
* Elasticsearchを検索バックエンドとして設定します。

1. 製品に 1000 を超える属性を作成する。
1. ファミリごとに製品を作成します。
1. インデクサーを実行します。

<u> 期待される結果：</u>

すべての商品がElasticsearchインデックスで使用できます。

<u> 実際の結果：</u>

1. Elasticsearchエラー：

   ```
    {"error":{"root_cause":[{"type":"illegal_argument_exception","reason":"Limit
    of total fields [3000] in index [magento2_product_2_v11] has been exceeded"}],"type":"illegal_argument_exception","reason":"Limit
    of total fields [3000] in index [magento2_product_2_v11] has been exceeded"},"status":400}
   ```

1. 新しい商品のインデックスが作成されませんでした。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
