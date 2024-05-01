---
title: 「MDVA-37182:Elasticsearch 6 と 7 で検索結果に一貫性がない」
description: MDVA-37182 パッチは、Elasticsearchのバージョン 6 と 7 で検索動作に一貫性がない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.22 がインストールされている場合に利用できます。 パッチ ID は MDVA-37182。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 6c4e2d2f-cced-487d-b253-fd0c80bc6067
feature: Search, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# MDVA-37182:Elasticsearch 6 と 7 で一致しない検索結果

MDVA-37182 パッチは、Elasticsearchのバージョン 6 と 7 で検索動作に一貫性がない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.22 がインストールされています。 パッチ ID は MDVA-37182。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.1～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

検索動作に一貫性がありません。

<u>再現手順</u>:

1. 次の詳細を持つ製品を作成します。
   * 名前：「5127AC」、「5127SS」、「5127AB」
   * SKU: 「product1」、「product2」、「product3」
1. 検索エンジンをElasticsearch 6 （ES6）に設定します。
1. 完全な再インデックスを実行します。
1. ストアフロントで「5127s」を検索します。
1. 検索エンジンをElasticsearch 7 （ES7）に設定します。
1. 完全な再インデックスを実行します。
1. ストアフロントで「5127s」を検索します。

<u>実際の結果：</u>:

ES6：検索で結果が返されません。ES7：検索で 3 つの製品が返されます。

<u>期待される結果：</u>:

検索では、両方のバージョンに対して 1 つの製品が返されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
