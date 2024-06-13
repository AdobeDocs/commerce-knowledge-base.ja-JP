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

MDVA-31307 パッチにより、次の問題が修正されます。 `Magento\_Csp/Model/BlockCache` は多くのメモリを消費し、大量のキャッシュ文字列を生成します。これにより、動的に許可リストに登録するスクリプトやスタイルが多数ある特定のページで問題が発生します。 提供されたパッチによって、このプロセスが最適化されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-31307。 この問題はAdobe Commerce 2.4.2 で修正されていることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.0 - 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

が存在する問題を修正しました *メモリ不足* キャッシュされたブロックの動的 CSP 許可リストへの登録に関する問題が原因で、特定のカテゴリでエラーが発生する。

<u>再現手順：</u>

1. 小さなプロファイル器具を生成する（`bin/magento setup:performance:generate-fixtures`）に設定します。
1. すべてのカテゴリページを異なるタブで開きます。

<u>実際の結果：</u>

*[日時] PHP 致命的なエラー：1073741824 バイトのメモリ サイズがライン 0 の Unknown で使い果たされました（90112 バイトの割り当てを試みました）
[日時] PHP 致命的エラー：/app/で 1073741824 バイトのメモリ サイズが使い果たされました（33554440 バイトの割り当てを試みました）`<project-id>`31 行目の/vendor/magento/module-csp/Model/Collector/DynamicCollector.php*

<u>期待される結果：</u>

すべてのページが正しく開きました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
