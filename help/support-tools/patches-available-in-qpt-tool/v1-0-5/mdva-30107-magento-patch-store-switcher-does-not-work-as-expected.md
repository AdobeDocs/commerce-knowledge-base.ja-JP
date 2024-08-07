---
title: 「MDVA-30107：ストアスイッチャーが期待どおりに動作しない」
description: MDVA-30107 パッチを適用すると、ストアビューに異なるベース URL が使用されている場合に、ストアスイッチャーが期待どおりに動作しない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.5 がインストールされている場合に利用できます。
exl-id: feaef9ed-615f-4a0a-a7c5-1833f993d27f
feature: Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# MDVA-30107：ストア スイッチャーが正常に動作しません

MDVA-30107 パッチを適用すると、ストアビューに異なるベース URL が使用されている場合に、ストアスイッチャーが期待どおりに動作しない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.5 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.0 - 2.3.5.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.3.0 ～ 2.3.5.x

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーがストアスイッチャーを使用してストアを切り替えると、ターゲットストアのベース URL が異なる場合、リクエストは失敗します。

<u> 再現手順 </u>:

1. 異なるベース URL を持つ 2 つ以上のストアを作成します。
1. これらの店舗のいずれかの店舗正面にあるカテゴリページに移動します。
1. ストア切り替えツールを使用して、別のストアに切り替えてみてください。

<u> 期待される結果 </u>:

別のストアの類似ページにリダイレクトされます。

<u> 実際の結果 </u>:

同じストアのホームページにリダイレクトされます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
