---
title: 「MDVA-40550：インデックス再作成後にフロントエンドに製品が表示されない」
description: MDVA-40550 パッチでは、インデックス再作成によって一部またはすべてのストアフロントカテゴリに製品が欠落する問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-40550。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 0aca6eb2-6eb2-4ac4-8ae1-052f671c14e5
feature: Categories, Console, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# MDVA-40550：インデックス再作成後にフロントエンドに製品が表示されない

MDVA-40550 パッチでは、インデックス再作成によって一部またはすべてのストアフロントカテゴリに製品が欠落する問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.6 がインストールされています。 パッチ ID は MDVA-40550。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 商品を作成します。
1. インデクサーをに切り替え **スケジュールで更新**.
   * 製品をカテゴリに割り当てます。
1. で xdebug を有効にして、xdebug ブレークポイントを設定します。 `\Magento\Indexer\Model\Indexer::reindexAll` および `\Magento\Indexer\Model\IndexMutex::execute`.
1. を実行 **フル再インデックス** 件中 `catalog_category_product` 次のコマンドを使用します。

   ```bash
   bin/magento indexer:reindex catalog_category_product
   ```

   * ブレークポイントで実行が停止するまで待ちます。 `\Magento\Indexer\Model\Indexer::reindexAll`.

1. 別のコンソールで、 **部分再インデックス** コマンドと並行して、次の操作を行います。

   ```bash
   bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1
   ```

1. ブレークポイントで実行が停止するまで待ちます。 `\Magento\Indexer\Model\IndexMutex::execute`. 次のロックが実行されます `catalog_category_product` インデクサー。
1. の完全な再インデックスの実行を再開 `catalog_category_product` ロックのタイムアウト（60 秒）を待ちます。

<u>期待される結果</u>:

コンソールにエラーメッセージはありません。

<u>実際の結果</u>:

次のエラーが発生します。

*インデックス catalog_category_product のロックを取得できませんでした。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
