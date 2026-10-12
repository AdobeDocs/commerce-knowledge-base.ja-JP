---
title: Adobe Commerce データベースの数値が範囲外です。「INT」から「BIGINT」
description: この記事では、価格の変更、削除、製品の複製など、製品の更新を保存できない場合の解決策を提供します。
exl-id: e2a00371-9032-4e81-b60e-5456ba35be94
feature: Services
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%
---
# Adobe Commerce データベースの数値が範囲外です。`INT` ～ `BIGINT`

>[!WARNING]
>
>この記事（`INT` ～ `BIGINT` スキーマの更新）のソリューションを実装する前に、マーチャントは常に、変更するフィールドが別のテーブルに対する外部キーの関係がないことを確認する必要があります。 フィールドに別のテーブルへの外部キーの関係がある場合、関連するフィールドがまだ`INT`であるため、問題が発生します。 次のクエリを使用して、これを検証できます。 このクエリは、特定のテーブルフィールドのデータベースで使用可能な外部キー関係をリストします。

```mysql
SELECT 
   TABLE_NAME,COLUMN_NAME,CONSTRAINT_NAME,REFERENCED_TABLE_NAME,REFERENCED_COLUMN_NAME
FROM
  INFORMATION_SCHEMA.KEY_COLUMN_USAGE
WHERE
   REFERENCED_TABLE_SCHEMA = '<database_name>' AND
   REFERENCED_TABLE_NAME = '<table_name>' AND
   REFERENCED_COLUMN_NAME = '<table_field>';
```

## 影響を受ける製品とバージョン

* Adobe Commerce （すべてのデプロイメント方法）すべての[&#x200B; サポートされているバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

この記事では、価格の変更、削除、製品の複製など、製品の更新を保存できない場合の解決策を提供します。
エラーメッセージ *在庫品目を保存できませんでした。 もう一度やり直してください。* 製品の更新後にデプロイできない場合があります。 `php bin/magento setup:upgrade`を実行すると、次の[!DNL MySQL] エラーメッセージが表示される場合もあります（Adobe Commerce on cloud infrastructureでは、このエラーがデプロイメントログに表示されます）。

```mysql
SQLSTATE[22003]: Numeric value out of range: 167 Out of range value for column 'value_id' at row 1, query was: INSERT INTO `catalog_product_entity_decimal` (`attribute_id`,`store_id`,`row_id`,`value`) VALUES (?, ?, ?, ?) ON DUPLICATE KEY UPDATE `attribute_id` = VALUES(`attribute_id`), `store_id` = VALUES(`store_id`), `row_id` = VALUES(`row_id`), `value` = VALUES(`value`)
```

記事に記載されている解決策は次のとおりです。

* `[ AUTO_INCREMENT ]`をテーブルから次の値に更新するか、または
* `INT` ～ `BIGINT` スキーマの更新

どのソリューションを使用するかは、問題の原因によって異なります。 原因を特定するには、次の手順を参照してください。

## 原因を確認する手順


ターミナルで次のコマンドを実行して、プライマリキーの最大値を確認します：`SELECT MAX(value_id) FROM catalog_product_entity_int;`

`max(value_id)`が`max int(11) [ 4294967296 ]`より低く、`[ AUTO_INCREMENT ]`の値が`max int(11) [ 4294967296 ]`以上である場合は、[&#x200B; テーブルから次の値に`[ AUTO_INCREMENT ]`を更新することを検討してください](#update-the-auto-increment-to-the-next-value-from-the-table)。 それ以外は、[`INT`から`BIGINT` スキーマの更新](#int_to_bigint_schema_update)を検討してください。

## `AUTO_INCREMENT`をテーブルの次の値に更新します {#update-the-auto-increment-to-the-next-value-from-the-table}

>[!WARNING]
>
>テーブルを変更する前に、データベースのバックアップを実行します。 また、サイトを[&#x200B; メンテナンスモード &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#maintenance-mode)にします。 さらに、変更を加えた後で、データベーステーブル（変更が行われたテーブルに対してのみ）で[!DNL MySQL] optimize コマンドを実行することをお勧めします。

>[!NOTE]
>
>特定のテーブルでoptimize コマンドを実行している間、サイトはメンテナンスモードである必要があります。 これにより、テーブルが完全に再構築され、テーブルからデータを削除した後に空き容量が増えます。

次のターミナル出力の例に示すように、表示される値が`max int(11) [ 4294967296 ]`より小さい場合、テーブル `[ AUTO_INCREMENT ]`が`max [ int(11) ]`の値より大きい数値に変更されています。

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

上記の例で示すように、テーブル `[ AUTO_INCREMENT ]`は`max int(11) [ 4294967296 ]`より大きな数に変更されました。 解決策は、`[ AUTO_INCREMENT]`をテーブルから次の値に更新することです。

```
ALTER TABLE catalog_product_entity_int AUTO_INCREMENT = 4283174131;
```

## `INT` ～ `BIGINT` スキーマの更新 {#int_to_bigint_schema_update}

ただし、次のクエリ `SELECT MAX(value_id) FROM catalog_product_entity_int;`を実行する場合、表示される値が`max int(11) [ 4294967296 ]`より大きい場合は、`INT` ～ `BIGINT` スキーマの更新を行うことを検討してください。 データ型`BIGINT`の値の範囲が広くなっています。

これを行うには：

1. *app/code/* ディレクトリ内にカスタムモジュールを作成します。
1. カスタムモジュールで、*db_schema.xml*&#x200B;を作成します。 *db_schema.xml*&#x200B;で、データタイプを`BIGINT`に設定します。
1. 次の内容を追加してから`bin/magento setup:upgrade`を実行し、上記の変更を対応するテーブルに適用します。

```
<?xml version="1.0"?>
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema.xsd">
    <table name="catalog_product_entity_int">
        <column xsi:type="bigint" name="value_id" unsigned="false" nullable="false" identity="true"
                comment="Value ID"/>
    </table>
</schema>
```


## 関連トピックス

* Commerce インストールガイドの[General [!DNL MySQL] guidelines](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql.html)
* [&#x200B; クラウドインフラストラクチャ上のAdobe Commerceのデータベースのベストプラクティス &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/database/database-best-practices-for-magento-commerce-cloud.html)
* [&#x200B; クラウドインフラストラクチャ上のAdobe Commerceのデータベースに関する最も一般的な問題](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/database/most-common-database-issues-in-magento-commerce-cloud.html) （サポートナレッジベース）
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
