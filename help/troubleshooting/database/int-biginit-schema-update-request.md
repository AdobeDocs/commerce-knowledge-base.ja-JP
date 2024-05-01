---
title: Adobe Commerce データベースの数値が範囲外です。「INT」から「BIGINT」
description: この記事では、価格の変更、製品の削除や複製など、製品の更新を保存できない場合のソリューションを説明します。
exl-id: e2a00371-9032-4e81-b60e-5456ba35be94
feature: Services
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Adobe Commerce データベースの数値が範囲外です。 `INT` 対象： `BIGINT`

>[!WARNING]
>
>この記事（）でソリューションを実装する前に`INT` 対象： `BIGINT` （スキーマの更新）マーチャントは、変更しようとしているフィールドが別のテーブルとの外部キー関係を持っていないことを常に確認する必要があります。 フィールドに別のテーブルへの外部キー関係がある場合、関連するフィールドがまだあるため、問題が発生します `INT`. 次のクエリを使用して、これを検証できます。 このクエリは、指定されたテーブル フィールドに対してデータベースで使用できる外部キー関係を一覧表示します。
>
```mysql
>SELECT 
>     TABLE_NAME,COLUMN_NAME,CONSTRAINT_NAME,REFERENCED_TABLE_NAME,REFERENCED_COLUMN_NAME
>FROM
>   INFORMATION_SCHEMA.KEY_COLUMN_USAGE
>WHERE
>     REFERENCED_TABLE_SCHEMA = '<database_name>' AND
>     REFERENCED_TABLE_NAME = '<table_name>' AND
>     REFERENCED_COLUMN_NAME = '<table_field>';
>```

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

この記事では、価格の変更、製品の削除や複製など、製品の更新を保存できない場合のソリューションを説明します。
エラーメッセージが表示される場合があります *在庫品目を保存できませんでした。 もう一度やり直してください。* 製品を更新した後、のデプロイに失敗する場合があります。 を実行すると、次の MySQL エラーメッセージも表示される場合があります `php bin/magento setup:upgrade` （クラウドインフラストラクチャ上のAdobe Commerceでは、このエラーはデプロイメントログに表示されます）。

```mysql
SQLSTATE[22003]: Numeric value out of range: 167 Out of range value for column 'value_id' at row 1, query was: INSERT INTO `catalog_product_entity_decimal` (`attribute_id`,`store_id`,`row_id`,`value`) VALUES (?, ?, ?, ?) ON DUPLICATE KEY UPDATE `attribute_id` = VALUES(`attribute_id`), `store_id` = VALUES(`store_id`), `row_id` = VALUES(`row_id`), `value` = VALUES(`value`)
```

この記事で説明する解決策は次のとおりです。
* を更新 `[ AUTO_INCREMENT ]` テーブルの次の値、または
* `INT` 対象： `BIGINT` スキーマの更新

使用するソリューションは、問題の原因によって異なります。 原因を特定するには、次の手順を参照してください。

## 原因を確認する手順


ターミナルで次のコマンドを実行して、プライマリキーの最大値を確認します。 `SELECT MAX(value_id) FROM catalog_product_entity_int;`

次の場合 `max(value_id)` 次より小さい `max int(11) [ 4294967296 ]`、および `[ AUTO_INCREMENT ]` 次より大きいか等しい値を持つ `max int(11) [ 4294967296 ]`では、次のことを考慮します [を更新しています `[ AUTO_INCREMENT ]` テーブルの次の値へ](#update-the-auto-increment-to-the-next-value-from-the-table). そうでない場合は、 [`INT` 対象： `BIGINT` スキーマの更新](#int_to_bigint_schema_update).

## を更新 `AUTO_INCREMENT` テーブルの次の値へ {#update-the-auto-increment-to-the-next-value-from-the-table}

>[!WARNING]
>
>テーブルを変更する前に、データベースのバックアップを実行します。 また、サイトをに配置します。 [メンテナンスモード](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#maintenance-mode). また、変更を加えた後で、データベーステーブル（変更が加えられたテーブルに対してのみ）に対して MYSQL optimize コマンドを実行することもお勧めします。

>[!NOTE]
>
>特定のテーブルに対して optimize コマンドを実行している間は、サイトをメンテナンスモードにする必要があります。 これにより、テーブルが完全に再構築され、テーブルからデータが削除された後に領域が解放されます。

表示される値がより小さい場合 `max int(11) [ 4294967296 ]` 次の例に示すように、テーブル以外の端子出力です `[ AUTO_INCREMENT ]` が、より大きい数または等しい数に変更されました `max [ int(11) ]` の値。

```mariadb
MariaDB [xxx]> SELECT MAX(value_id) FROM catalog_product_entity_int;
+---------------------+
| MAX(source_item_id) |
+---------------------+
|          4283174130 |
+---------------------+
```

これが発生したかどうかを確認するには、ターミナルで次のコマンドを実行します。

```
MariaDB [xxx]> show create table catalog_product_entity_int;

...
) ENGINE=InnoDB AUTO_INCREMENT=4294967297 DEFAULT CHARSET=utf8 COMMENT='Catalog Product Integer Attribute Backend Table';
```

上記の例でわかるように、テーブルを出力します `[ AUTO_INCREMENT ]` がを超える数に変更されました `max int(11) [ 4294967296 ]`. 解決策は、 `[ AUTO_INCREMENT]` をテーブルの次の値に変更します。

```
ALTER TABLE catalog_product_entity_int AUTO_INCREMENT = 4283174131;
```

## `INT` 対象： `BIGINT` スキーマの更新 {#int_to_bigint_schema_update}

ただし、次のクエリを実行する場合は `SELECT MAX(value_id) FROM catalog_product_entity_int;` 表示される値がより大きい `max int(11) [ 4294967296 ]`  ～を行うことを検討する `INT` 対象： `BIGINT` スキーマの更新。 データタイプ `BIGINT` には、より大きな値の範囲があります。

それには、以下の手順を実行します。

1. 内にカスタムモジュールを作成 *app/code/* ディレクトリ。
1. カスタムモジュールで、 *db_schema.xml*. 対象： *db_schema.xml* データタイプをに設定します `BIGINT`.
1. 次のコンテンツを追加して、を実行します `bin/magento setup:upgrade` をクリックして、上記の変更を対応するテーブルに適用します。

```
<?xml version="1.0"?>
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="catalog_product_entity_int">
        <column xsi:type="bigint" name="value_id" unsigned="false" nullable="false" identity="true"
                comment="Value ID"/>
    </table>
</schema>
```


## 関連資料

* [一般的な MySQL ガイドライン](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql.html) （Commerce インストールガイド）を参照してください。
* [データベースのアップロードにより MySQL への接続が失われる](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/database-upload-loses-connection-to-mysql.html) サポートナレッジベースで。
* [クラウドインフラストラクチャー上のAdobe Commerceに関するデータベースのベストプラクティス](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/database/database-best-practices-for-magento-commerce-cloud.html) サポートナレッジベースで。
* [クラウドインフラストラクチャー上のAdobe Commerceで最も一般的なデータベースの問題](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/database/most-common-database-issues-in-magento-commerce-cloud.html) サポートナレッジベースで。
