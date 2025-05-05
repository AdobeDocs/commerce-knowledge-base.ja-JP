---
title: Elasticsearch 5 が設定され、「Fielddata が無効になっています…」エラーで検索ページが読み込まれない
description: 「ここでは、Elasticsearch 5 で検索ページが読み込まれず、次のような例外が発生する問題を修正する方法について説明します。」
exl-id: f5fa8144-4e7c-45ce-89d0-a8367e91d6db
feature: Cache
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Elasticsearch 5 が設定され、「Fielddata が無効になっています…」エラーで検索ページが読み込まれない

ここでは、Elasticsearch 5 で検索ページが読み込まれず、次のような例外が発生する問題を修正する方法について説明します。

```bash
{"0":"{\"error\":{\"root_cause\":[{\"type\":\"illegal_argument_exception\",\"reason\":\"Fielddata is disabled on text fields by default. Set fielddata=true on [%attribute_code%]] in order to load fielddata in memory by uninverting the inverted index. Note that this can however use significant memory.\"}].
```

## 影響を受けるバージョン

* Adobe Commerce 2.2.x
* Elasticsearch v.5

>[!NOTE]
>
>Adobe Commerce 2.3.x のElasticsearch v.5 は非推奨（廃止予定）になりました

## 問題

前提条件：Elasticsearch 5 が設定されていること。

検索リクエストで、次の例外がログに生成されます。

```bash
{"0":"{\"error\":{\"root_cause\":[{\"type\":\"illegal_argument_exception\",\"reason\":\"Fielddata is disabled on text fields by default. Set fielddata=true on [%attribute_code%]] in order to load fielddata in memory by uninverting the inverted index. Note that this can however use significant memory.\"}].
```

## 原因：

デフォルトでは、レイヤーナビゲーションで使用できるのは、特定のタイプの製品属性のみです。 「Yes/No」、「Dropdown」、「Multipleselect」、「Price」です。 そのため、Commerce Admin では、他のタイプの属性を **レイヤーナビゲーションで使用** = *フィルタリング可能* または **検索結果レイヤーナビゲーションで使用** = *はい* に設定することはできません。 ただし、データベース内の `is_filterable` と `is_filterable_in_search` の値を直接変更することで、この制限を回避する技術的な可能性があります。 これが発生し、日付やテキストなどの他の属性タイプがレイヤーナビゲーションで使用されるように設定されている場合、Elasticsearch 5 は例外をスローします。

これを実現するには、レイヤーナビゲーションで使用するように設定されている Dropdown、Multipleselect、Price 以外の属性があるかどうかを確認する必要があります。 次のクエリを実行して、これらの属性を検索します。

```sql
SELECT ea.attribute_code, ea.frontend_input, cea.is_filterable, cea.is_filterable_in_search FROM eav_attribute AS ea
    -> INNER JOIN catalog_eav_attribute AS cea ON ea.attribute_id = cea.`attribute_id`
    -> WHERE (is_filterable = 1 OR is_filterable_in_search = 1) AND frontend_input NOT IN ('boolean', 'multiselect', 'select', 'price');
```

結果には、レイヤーナビゲーションに使用される属性のリストが含まれます。このタイプでは、これを許可していません。 この問題を修正するには、次の節で説明する手順を実行します。

## 解決策

この問題を修正するには、`is_filterable` （レイヤーナビゲーションで使用）および `filterable_in_search` （検索結果レイヤーナビゲーションで使用）を「0」（使用しない）に設定する必要があります。 これを行うには、次の手順を実行します。

1. データベースバックアップを作成します。
1. [phpMyAdmin](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin) などのデータベースツールを使用するか、コマンドラインから手動で DB にアクセスして、次の SQL クエリを実行します。

   ```sql
   UPDATE catalog_eav_attribute AS cea
       INNER JOIN eav_attribute AS ea
           ON ea.attribute_id = cea.attribute_id
   SET cea.is_filterable = 0, cea.is_filterable_in_search = 0
   WHERE (cea.is_filterable = 1 OR cea.is_filterable_in_search = 1)
       AND frontend_input NOT IN ('boolean', 'multiselect', 'select', 'price');
   ```

1. 次のコマンドを使用して、カタログ検索の完全な再インデックスを実行します。

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. 次を実行してキャッシュをクリーンアップ

   ```bash
   bin/magento cache:clean
   ```

または、Commerce管理の **システム**/**ツール**/**キャッシュ管理** で設定します。

これで、問題なくカタログ検索を実行できるようになります。
