---
title: Adobe Commerce データベースの数値が範囲外です。「INT」から「BIGINT」
description: この記事では、価格の変更、製品の削除や複製など、製品の更新を保存できない場合のソリューションを説明します。
exl-id: e2a00371-9032-4e81-b60e-5456ba35be94
feature: Services
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---

# Adobe Commerce データベースの数値が範囲外です（`INT` ～ `BIGINT`）

>[!WARNING]
>
>この記事（スキーマの更新に `INT` る）のソリューションを実装す `BIGINT` 前に、マーチャントは、変更しようとしているフィールドに別のテーブルへの外部キー関係がないことを常に確認する必要があります。 フィールドに別のテーブルへの外部キー関係がある場合、関連するフィールドがまだ `INT` しいため、問題が発生します。 次のクエリを使用して、これを検証できます。 このクエリは、指定されたテーブル フィールドに対してデータベースで使用できる外部キー関係を一覧表示します。
>
>```mysql
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

* Adobe Commerce（すべてのデプロイメント方法）すべてのバージョン [ サポートされているバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

この記事では、価格の変更、製品の削除や複製など、製品の更新を保存できない場合のソリューションを説明します。
「在庫項目を保存できませんでした *というエラーメッセージが表示される場合があります。 もう一度やり直してください。* 製品を更新した後、デプロイに失敗する場合があります。 `php bin/magento setup:upgrade` を実行すると、次の [!DNL MySQL] エラーメッセージが表示される場合もあります（クラウドインフラストラクチャ上のAdobe Commerceでは、このエラーがデプロイメントログに表示されます）。

```mysql
SQLSTATE[22003]: Numeric value out of range: 167 Out of range value for column 'value_id' at row 1, query was: INSERT INTO `catalog_product_entity_decimal` (`attribute_id`,`store_id`,`row_id`,`value`) VALUES (?, ?, ?, ?) ON DUPLICATE KEY UPDATE `attribute_id` = VALUES(`attribute_id`), `store_id` = VALUES(`store_id`), `row_id` = VALUES(`row_id`), `value` = VALUES(`value`)
```

この記事で説明する解決策は次のとおりです。
* テーブルの次の値に `[ AUTO_INCREMENT ]` を更新する、または
* `INT` から `BIGINT` スキーマの更新

使用するソリューションは、問題の原因によって異なります。 原因を特定するには、次の手順を参照してください。

## 原因を確認する手順


ターミナルで次のコマンドを実行して、プライマリキーの最大値を確認します。`SELECT MAX(value_id) FROM catalog_product_entity_int;`

`max(value_id)` が `max int(11) [ 4294967296 ]` よりも小さく、`[ AUTO_INCREMENT ]` の値が `max int(11) [ 4294967296 ]` 以上の場合は、[ テーブルの次の値に `[ AUTO_INCREMENT ]` を更新する ](#update-the-auto-increment-to-the-next-value-from-the-table) ことを検討してください。 それ以外の場合は、スキーマの更新 `BIGINT` の [`INT` を検討します ](#int_to_bigint_schema_update)。

## `AUTO_INCREMENT` をテーブルの次の値に更新します {#update-the-auto-increment-to-the-next-value-from-the-table}

>[!WARNING]
>
>テーブルを変更する前に、データベースのバックアップを実行します。 また、サイトを [ メンテナンスモード ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html?lang=ja#maintenance-mode) にします。 また、変更を加えた後で、データベーステーブルに対して（変更が加えられたテーブルに対してのみ） [!DNL MySQL] optimize コマンドを実行することもできます。

>[!NOTE]
>
>特定のテーブルに対して optimize コマンドを実行している間は、サイトをメンテナンスモードにする必要があります。 これにより、テーブルが完全に再構築され、テーブルからデータが削除された後に領域が解放されます。

次の端子出力例に示すように、表示される値が `max int(11) [ 4294967296 ]` より小さい場合は、`max [ int(11) ]` の値より大きいか等しい数に変更され `[ AUTO_INCREMENT ]` テーブルよりも小さい値になります。

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

上記の例でわかるように、テーブル `[ AUTO_INCREMENT ]` が `max int(11) [ 4294967296 ]` よりも大きい数に変更されたことを出力します。 解決策は、テーブルの次の値に `[ AUTO_INCREMENT]` を更新することです。

```
ALTER TABLE catalog_product_entity_int AUTO_INCREMENT = 4283174131;
```

## `INT` から `BIGINT` スキーマの更新 {#int_to_bigint_schema_update}

ただし、次のクエリを実行する際に、表示され `SELECT MAX(value_id) FROM catalog_product_entity_int;` 値がを超える場合は、スキーマの更新を `INT` 行 `max int(11) [ 4294967296 ]` ることを検討してくだ `BIGINT` い。 データタイプ `BIGINT` には、より大きな値の範囲があります。

それには、以下の手順を実行します。

1. *app/code/* ディレクトリ内にカスタムモジュールを作成します。
1. カスタムモジュールで、*db_schema.xml* を作成します。 *db_schema.xml では* データタイプを `BIGINT` に設定します。
1. 次のコンテンツを追加し、`bin/magento setup:upgrade` を実行して、上記の変更を対応するテーブルに適用します。

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

* Commerce インスト  [!DNL MySQL]  ルガイドの [ 一般的なガイドライン ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql.html?lang=ja)
* サポートナレッジベースの [ データベースのアップロードにより  [!DNL MySQL]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/database-upload-loses-connection-to-mysql.html?lang=ja) への接続が失われる
* [ クラウドインフラストラクチャー上のAdobe Commerceに関するデータベースのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/database/database-best-practices-for-magento-commerce-cloud.html?lang=ja) に関するサポートナレッジベース
* [ クラウドインフラストラクチャー上のAdobe Commerceにおける最も一般的なデータベースの問題 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/database/most-common-database-issues-in-magento-commerce-cloud.html?lang=ja) については、サポートナレッジベースを参照してください
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
