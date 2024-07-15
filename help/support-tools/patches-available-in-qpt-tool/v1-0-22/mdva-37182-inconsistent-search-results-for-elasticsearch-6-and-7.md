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

MDVA-37182 パッチは、Elasticsearchのバージョン 6 と 7 で検索動作に一貫性がない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.22 がインストールされている場合に使用できます。 パッチ ID は MDVA-37182。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.1～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

検索動作に一貫性がありません。

<u> 再現手順 </u>:

1. 次の詳細を持つ製品を作成します。
   * 名前：「5127AC」、「5127SS」、「5127AB」
   * SKU: 「product1」、「product2」、「product3」
1. 検索エンジンをElasticsearch 6 （ES6）に設定します。
1. 完全な再インデックスを実行します。
1. ストアフロントで「5127s」を検索します。
1. 検索エンジンをElasticsearch 7 （ES7）に設定します。
1. 完全な再インデックスを実行します。
1. ストアフロントで「5127s」を検索します。

<u> 実際の結果：</u>

ES6：検索で結果が返されません。ES7：検索で 3 つの製品が返されます。

<u> 期待される結果：</u>:

検索では、両方のバージョンに対して 1 つの製品が返されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
