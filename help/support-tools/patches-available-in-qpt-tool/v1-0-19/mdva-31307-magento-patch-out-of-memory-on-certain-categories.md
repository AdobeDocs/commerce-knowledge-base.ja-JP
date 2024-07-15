---
title: 「MDVA-31307：特定のカテゴリのメモリ不足」
description: MDVA-31307 パッチは、「Magento\_Csp/Model/BlockCache」が大量のメモリを消費し、大量のキャッシュされた文字列を生成し、動的な許可リストのスクリプトやスタイルの多い特定のページで問題を引き起こす問題を修正します。 提供されたパッチによって、このプロセスが最適化されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-31307。 この問題はAdobe Commerce 2.4.2 で修正されていることに注意してください。
exl-id: 15d82f5b-bd43-4a0a-b756-d109dac6d2cd
feature: Cache, Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# MDVA-31307：特定のカテゴリのメモリ不足

MDVA-31307 パッチは、`Magento\_Csp/Model/BlockCache` が大量のメモリを消費し、大量のキャッシュ文字列を生成する問題を修正します。これにより、動的に許可リストに登録されるスクリプトやスタイルが大量に存在する特定のページで問題が発生します。 提供されたパッチによって、このプロセスが最適化されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.19 がインストールされている場合に使用できます。 パッチ ID は MDVA-31307。 この問題はAdobe Commerce 2.4.2 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**このパッチは、Adobe Commerce バージョン用に作成されます** Adobe Commerce on cloud infrastructure 2.4.0

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.0～2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

キャッシュされたブロックの動的 CSP 許可リストへの登録に関する問題が原因で、特定のカテゴリで *メモリ不足* エラーが発生する問題を修正しました。

<u> 再現手順：</u>

1. 小さなプロファイル器具（`bin/magento setup:performance:generate-fixtures`）を生成します。
1. すべてのカテゴリページを異なるタブで開きます。

<u> 実際の結果：</u>

*[日付と時刻 ] PHP 致命的エラー：1073741824 バイトのメモリ サイズが使い果たされました（90112 バイトの割り当てを試みました） （行 0 の不明）
[ 日付と時刻 ] PHP 致命的エラー：31 行目の/app/`<project-id>`/vendor/magento/module-csp/Model/Collector/DynamicCollector.phpで、1073741824 バイトのメモリサイズが使い果たされました（33554440 バイトの割り当てを試みました）*

<u> 期待される結果：</u>

すべてのページが正しく開きました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) の節を参照してください。
