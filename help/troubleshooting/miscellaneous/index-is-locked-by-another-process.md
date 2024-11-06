---
title: インデックスは別のプロセスによってロックされています
description: この記事では、インデックスが別のプロセスによってロックされ、スキップされる、Adobe Commerceの一般的なインデックス作成の問題について説明します。
exl-id: 542c714c-fad5-4f0e-9757-d90044c36bfc
feature: Catalog Management, Categories
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# インデックスは別のプロセスによってロックされています

この記事では、インデックスが別のプロセスによってロックされ、スキップされる、Adobe Commerceの一般的なインデックス作成の問題について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.X

## 問題

CLI での完全なインデックス再作成中に、Adobe Commerceで「*&#39;Index is locked by another reindex process. スキップしています。&#39;* つまり、プロセスまたはインデックスタイプがロックされている場合、ロックされた特定のインデックスタイプを再インデックス化することはできません。 再インデックスは、常にそのインデックスタイプをスキップします。

## 原因：

このエラーは、前のインデックスが正常に完了しなかった場合に発生する可能性があります。 考えられる理由は次のとおりです。

* プロセスが別のプロセスまたはユーザーによって中断されました。
* メモリ制限。
* タイムアウトなどの MySQL エラー。
* 再インデックス中に致命的な PHP エラーが発生しました。

## 再現手順

1. 例えば、    ```bash    cataloginventory_stock ```    インデックスタイプがロックされています。
1. CLI コマンドを実行してすべてのデータを再インデックスする場合    ```bash    php bin/magento indexer:reindex    ``` の場合、次の出力結果が得られます。    ```bash    customer_grid index has been rebuilt successfully in 00:00:09    catalog_category_product index has been rebuilt successfully in 00:00:07    catalog_product_category index has been rebuilt successfully in 00:00:00    catalogrule_rule index has been rebuilt successfully in 00:00:05    catalog_product_attribute index has been rebuilt successfully in 00:00:04    cataloginventory_stock index is locked by another reindex process. Skipping.    catalog_product_price index has been rebuilt successfully in 00:00:01    catalogrule_product has been rebuilt successfully in 00:00:00    catalogsearch_fulltext index has been rebuilt successfully in 00:00:01    ```
1. 上記のように、    ```bash    cataloginventory_stock```    インデックスプロセスはスキップされました。


## 解決策

インデックスのステータスをリセットしてから、新しいインデックス再作成プロセスを実行する必要があります。 インデックスのリセットステータスについては、次のコマンドを実行する必要があります。

```bash
bin/magento indexer:reset <index identifier>
```

インデックス識別子（コード）が不明な場合は、次のコマンドを使用してリストできます。

```bash
bin/magento indexer:info
```

完全性のために、ネイティブインデックスのすべての組み合わせを次に示します。

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


## 関連資料

サポートナレッジベースでは、

* [Cron タスクが他のグループからタスクをロック（クラウドインフラストラクチャ上のAdobe Commerce）](/help/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.md)

このユーザーガイドで、

* [ インデックスの管理 ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management?itm_source=merchdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=reindexing)

開発者向けドキュメントでは、

* [ インデックス作成の概要 ](https://developer.adobe.com/commerce/php/development/components/indexing/)
* [ インデクサーのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/performance-best-practices/configuration)
* [Cron の設定と実行 ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)
* [ インデクサーの管理 ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)
* [ インデクサーの最適化 ](https://developer.adobe.com/commerce/php/development/components/indexing/optimization/)
