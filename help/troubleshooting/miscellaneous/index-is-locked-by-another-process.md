---
title: インデックスは別のプロセスによってロックされています
description: この記事では、インデックスが別のプロセスによってロックされ、スキップされるAdobe Commerceの一般的なインデックス作成の問題について説明します。
exl-id: 542c714c-fad5-4f0e-9757-d90044c36bfc
feature: Catalog Management, Categories
role: Developer
source-git-commit: 1536ad8672498cf36f3d28452762744e4ffcc5de
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# インデックスは別のプロセスによってロックされています

この記事では、インデックスが別のプロセスによってロックされ、スキップされるAdobe Commerceの一般的なインデックス作成の問題について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.X

## イシュー

CLIの完全なインデックス再作成中に、Adobe Commerceでエラーメッセージが表示されます。*&#39;インデックスは別のインデックス再作成プロセスによってロックされています。 スキップしています。&#39;* プロセスまたはインデックスタイプがロックされている場合、特定のロックされたインデックスタイプを再インデックス化することはできません。 インデックス再作成は、常にそのインデックスタイプをスキップします。

## 原因

このエラーは、前のインデックスが正常に完了しなかった場合に発生する可能性があります。 考えられる理由は次のとおりです。

* プロセスが別のプロセスまたはユーザーによって中断されました。
* メモリ制限。
* タイムアウトなどのMySQL エラー。
* 再インデックス中に致命的なPHP エラーが発生しました。

## 複製の手順

1. 例えば、`cataloginventory_stock` インデックスタイプがロックされているとします。
1. CLI コマンドを実行して、すべてのデータを再インデックス化しようとすると、次の操作が実行されます。

   ```bash
   php bin/magento indexer:reindex
   ```

   次の出力結果が得られます。

   ```
   customer_grid index has been rebuilt successfully in 00:00:09
   catalog_category_product index has been rebuilt successfully in 00:00:07
   catalog_product_category index has been rebuilt successfully in 00:00:00
   catalogrule_rule index has been rebuilt successfully in 00:00:05
   catalog_product_attribute index has been rebuilt successfully in 00:00:04
   cataloginventory_stock index is locked by another reindex process. Skipping.
   catalog_product_price index has been rebuilt successfully in 00:00:01
   catalogrule_product has been rebuilt successfully in 00:00:00
   catalogsearch_fulltext index has been rebuilt successfully in 00:00:01
   ```

1. 上に示すように、`cataloginventory_stock` インデックスプロセスはスキップされています。

## Solution

インデックスのステータスをリセットしてから、新しいインデックス再作成プロセスを実行する必要があります。 インデックスのステータスをリセットするには、次のコマンドを実行する必要があります。

```bash
bin/magento indexer:reset <index identifier>
```

インデックス識別子（コード）がわからない場合は、次のコマンドを使用してリスト化できます。

```bash
bin/magento indexer:info
```

完全性を確保するために、ネイティブインデックスの可能なすべての組み合わせを次に示します。

```bash
bin/magento indexer:reset design_config_grid;
bin/magento indexer:reset customer_grid;
bin/magento indexer:reset catalog_category_product;
bin/magento indexer:reset catalog_product_category;
bin/magento indexer:reset catalogrule_rule;
bin/magento indexer:reset catalog_product_attribute;
bin/magento indexer:reset cataloginventory_stock;
bin/magento indexer:reset catalog_product_price;
bin/magento indexer:reset catalogrule_product;
bin/magento indexer:reset catalogsearch_fulltext;
```

## 関連トピックス

サポートナレッジベース：

* [Cron タスクは、他のグループからタスクをロックします（Adobe Commerce on cloud infrastructure）](/help/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.md)

アドビのユーザーガイドの内容：

* [インデックス管理](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/index-management?itm_source=merchdocs&itm_medium=search_page&itm_campaign=federated_search&itm_term=reindexing)

アドビの開発者ドキュメントには、次のようなものがあります。

* [インデックス作成の概要](https://developer.adobe.com/commerce/php/development/components/indexing/)
* [インデクサーのベストプラクティス](https://experienceleague.adobe.com/ja/docs/commerce-operations/performance-best-practices/configuration)
* [Cronの設定と実行](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)
* [インデクサーの管理](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers)
* [インデクサーの最適化](https://developer.adobe.com/commerce/php/development/components/indexing/optimization/)
