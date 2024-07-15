---
title: 「MDVA-28993:Elasticsearch部分検索、「最小値は一致する必要があります」および「ハイフンを使用した検索」の問題を修正」
description: MDVA-28993 パッチは、「Minimum should match」機能とElasticsearch エンジンの部分検索を実装し、検索クエリでのハイフンの問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） v.1.0.6 がインストールされている場合に利用できます。
exl-id: 2af0f950-284b-42f2-9660-8aafce4b04d7
feature: Search, Services
role: Admin
source-git-commit: 6f4d6382cbdb7bedddcc3f264fbf6ef997729323
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# MDVA-28993:Elasticsearch部分検索。「最小値は一致する必要がある」で「ハイフンを使用した検索」の問題を修正

MDVA-28993 パッチは、「Minimum should match」機能とElasticsearch エンジンの部分検索を実装し、検索クエリでのハイフンの問題を解決します。 パッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.6 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.4 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミス/Adobe Commerce on cloud infrastructure 2.3.4-2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。


## 問題

Elasticsearch 6 でハイフン（–）を含む SKU を検索すると、返される結果が多すぎます。

<u> 再現手順：</u>

1. ストアフロントに移動します。

1. 検索バーに、ハイフンを含む文字列（例：「WS-M-Blue」）を入力します。

<u> 期待される結果：</u>

WS-M-Blue のみを返します。

<u> 実際の結果：</u>

「WS」で始まるすべての SKU を返します。

## パッチの詳細

MDVA-28993 パッチには、以下の修正および改善点が含まれています。

* は、新しい「一致する必要がある最小値」機能と、Elasticsearchエンジンの部分検索を実装します。 設定について詳しくは、ユーザーガイドの [ カタログ検索の設定 ](https://docs.magento.com/user-guide/catalog/search-configuration.html#step-4-configure-minimum-terms-to-match) を参照してください。
* Elasticsearchの部分検索
* 前述の「ハイフンを使用した検索」の問題を修正しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
