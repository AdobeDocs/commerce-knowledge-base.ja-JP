---
title: 「MDVA-41139：製品の読み込み後、設定可能な製品の在庫切れになる」
description: MDVA-41139 パッチは、そのソースの 1 つに対する単純な製品の qty = 0 の場合、製品のインポート後に設定可能な製品が在庫切れになる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.8 がインストールされている場合に利用できます。 パッチ ID は MDVA-41139。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: e90ab578-50b9-4bc4-baf9-de4182e700ae
feature: Data Import/Export, Configuration, Orders, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# MDVA-41139：製品のインポート後に、設定可能な製品が在庫切れになる

MDVA-41139 パッチは、そのソースの 1 つに対する単純な製品の qty = 0 の場合、製品のインポート後に設定可能な製品が在庫切れになる問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.8 がインストールされている場合に使用できます。 パッチ ID は MDVA-41139。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

製品のインポート後、そのソースの 1 つに対する単純製品の数量= 0 の場合、設定可能な製品は在庫切れになります。

<u> 前提条件 </u>:

インベントリモジュールがインストールされます。

<u> 再現手順 </u>:

1. 新しいソースと在庫を作成します。
1. デフォルトソースと新しいソースに割り当てられた子製品を持つ設定可能なプロダクトを作成します。
1. 各子製品のデフォルト在庫の値を 0 に、その他の在庫を 0 に設定します。
1. 設定可能な商品が在庫にあります。
1. この製品をエクスポートしてから、もう一度インポートしてください。

<u> 期待される結果 </u>:

2 番目のソースの数量が 0 を超えているので、設定可能な製品は在庫にあります。

<u> 実際の結果 </u>:

設定可能な商品の在庫がありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
