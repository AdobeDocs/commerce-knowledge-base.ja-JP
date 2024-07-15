---
title: 「MDVA-31224 パッチ：製品価格の再インデックスに時間がかかる」
description: MDVA-31224 パッチは、製品価格の再インデックスが完了するまでに時間がかかりすぎたり、完了しない場合の問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） v.1.0.7 がインストールされている場合に利用できます。
exl-id: 17f83fbf-9a43-4a65-b560-5f729b037c17
feature: Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# MDVA-31224 パッチ：製品価格の再インデックスに時間がかかりすぎる

MDVA-31224 パッチは、製品価格の再インデックスが完了するまでに時間がかかりすぎたり、完了しない場合の問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) v.1.0.7 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャー 2.3.3 上のAdobe Commerce用に設計されました。
* このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.3 - 2.3.4-p2 とも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品価格の再インデックスが完了するまでに時間がかかりすぎる、または完了しない。

<u> 再現手順：</u>

1. 15 種類のオプションから選択できる 6000 個のバンドル製品を作成します。
1. 30 個のオプションを持つ 1 つのバンドル製品を作成します。
1. CLI から price reindex を実行します。     `bin/magento indexer:reindex catalog_product_price`

<u> 期待される結果：</u>

製品価格の再インデックスは、完了するまで 1.5 時間以上かかります。

<u> 実績：</u>

製品価格の再インデックスが完了するまでに短い時間（1 ～ 2 分）がかかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
