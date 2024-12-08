---
title: データ移行ツールのトラブルシューティング
description: この記事では、データ移行ツールの実行時に発生する可能性のあるエラーの解決策について説明します。
exl-id: 9beb31ae-ed3c-42e1-b0bf-33fb1c91e0ea
feature: Data Import/Export
role: Developer
source-git-commit: 958067830d32b1f10ffa669307ec76d1e14b82a4
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# データ移行ツールのトラブルシューティング

この記事では、データ移行ツールの実行時に発生する可能性のあるエラーの解決策について説明します。

## Source ドキュメント/フィールドがマッピングされていない {#source-documents-fields-not-mapped}

### エラーメッセージ

* ```bash    Source documents are not mapped: <EXTENSION_TABLE>    ```
* ```bash    Source fields are not mapped. Document: <EXTENSION_TABLE>. Fields: <EXTENSION_FIELD>    ```

まれに、次のようなメッセージが表示されます

```bash
Destination documents
```

または

```bash
Destination fields
```

ソースの代わりに使用します。

### 原因：

一部のAdobe Commerce バージョン 1 エンティティ（ほとんどの場合、拡張機能から取得）は、Adobe Commerce バージョン 2 データベースに存在しません。

このメッセージが表示されるのは、Data Migration Tool が内部テストを実行して、テーブルとフィールドが *source* （Adobe Commerce 1）および *destination* （Adobe Commerce 2）データベース間で一致していることを確認するためです。

### 可能な解決策

* 対応するAdobe Commerce 2 拡張機能を [Commerce Marketplace](https://marketplace.magento.com/) からインストールします。     競合するデータの発行元が独自のデータベース構造要素を追加する拡張機能の場合、同じ拡張機能のAdobe Commerce 2 バージョンは、対象の（Adobe Commerce 2） データベースにこのような要素を追加し、問題を解決する可能性があります。
* ツールを実行する際は `-a` 引数を使用して、エラーを自動解決し、移行が停止しないようにします。
* 問題のあるデータを無視するようにツールを設定します。

データベースエンティティを無視するには、次のように、`<ignore>` タグを `map.xml` ファイル内のエンティティに追加します。

```xml
...
    <source>
        <document_rules>
            ...
            <!-- Ignore `sales_flat_invoice_grid` table -->
            <ignore>
                <document>sales_flat_invoice_grid</document>
            </ignore>
            <!-- Ignore `address_id` field of `sales_flat_order_address` table -->
            <ignore>
                <field>sales_flat_order_address.address_id</field>
            </ignore>
            ...
        </document_rules>
    </source>
    ...
```

>[!WARNING]
>
>マップファイルまたは「`-a`」オプションを使用してエンティティを無視する前に、影響を受けるデータをAdobe Commerce 2 ストアに置く必要がないことを確認してください。

## クラスがレコードにマッピングされていません {#class-does-not-exist-but-mentioned}

### エラーメッセージ

```bash
Class <extension/class_name> is not mapped in record <attribute_id=196>
```

### 原因：

開発者向けドキュメントの [EAV 移行手順 ](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/data-migration/basics/technical-specification) 中に、Adobe Commerce 1 コードベースのクラスがAdobe Commerce 2 コードベースに見つかりませんでした。 ほとんどの場合、欠落しているクラスは [extension](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#extension) に属しています。

### 可能な解決策

* 対応するAdobe Commerce 2 拡張機能をインストールします。
* 問題の原因となった属性を無視します。    この場合は、`eav-attribute-groups.xml.dist` ファイルの `ignore` グループに属性を追加します。
* `class-map.xml.dist` ファイルを使用して、クラスマッピングを追加します。

## 外部キー制約に失敗します

### エラーメッセージのテキスト

```bash
Foreign key <KEY_NAME> constraint fails on source database. Orphan records id: <id_1>, <id_2> from <child_table>.<field_id> has no referenced records in <parent_table>
```

### 原因：

`child_table` の `field_id` が指している `parent_table` にデータベース レコードがありません。

### 考えられる解決策

レコードが必要ない場合は、`child_table` から削除します。

レコードを保持するには、データ移行ツールの `config.xml` を変更して `Data Integrity Step` を無効にします。

## URL リライトの重複

```xml
There are duplicates in URL rewrites:
Request path: towel.html Store ID: 2 Target path: catalog/product/view/id/10
Request path: towel.html Store ID: 2 Target path: catalog/product/view/id/12
```

### 原因：

URL 書き換えの `Target path` は、`Request path` + `Store ID` の一意のペアで指定する必要があります。 このエラーは、同じ `Request path` と `Store ID` のペアを 2 つの異なる `Target path` 値で使用する 2 つのエントリを報告します。

### 考えられる解決策

`config.xml` ファイルで「`auto_resolve_urlrewrite_duplicates`」オプションを有効にします。

この設定は、URL 書き換えの競合するレコードにハッシュ文字列を追加し、コマンドラインインターフェイスに解決結果を表示します。

## エンティティの不一致 {#mismatch-of-entities}

### エラーメッセージ

```bash
Mismatch of entities in the document: <DOCUMENT> Source: <COUNT_ITEMS_IN_SOURCE_TABLE> Destination: <COUNT_ITEMS_IN_DESTINATION_TABLE>
```

### 原因：

エラーは、ボリュームチェックの手順で発生。 つまり、ドキュメントのAdobe Commerce 2 データベースレコード数は、Adobe Commerce 1 と同じではありません。

レコードの欠落は、顧客が移行中に注文を行った場合に発生します。

### 考えられる解決策

データ移行ツールを `Delta` モードで実行して、増分変更を転送します。

## Deltalog がインストールされていません {#deltalog-is-not-installed}

### エラーメッセージ

```bash
Deltalog for <TABLE_NAME> is not installed
```

### 原因：

このエラーは、（開発者向けドキュメントの [ 増分移行 ](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/data-migration/migrate-data/delta) データに対する変更の際に発生します。 つまり、deltalog テーブル（プレフィックス `m2_cl_*` を含む）がAdobe Commerce 1 データベースに見つかりませんでした。 このツールは、（アドビの開発者向けドキュメントの [data migration](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/data-migration/migrate-data/data) 中にこれらのテーブルをインストールするだけでなく、変更内容を追跡して deltalog テーブルに値を入力するデータベーストリガーもインストールします。

このエラーの理由の 1 つは、ライブストア自体からではなく、ライブ Adobe Commerce 1 ストアの *コピー* から移行しようとしていることです。 一度も移行されていないライブ Adobe Commerce 1 ストアからコピーを作成すると、そのコピーには、差分マイグレーションを行うのに必要なトリガーや追加の差分テーブルが含まれないので、マイグレーションが失敗します。 データ移行ツールでは、AC1 と AC2 の DB を比較して相違点を移行しません。 代わりに、最初のマイグレーション時にインストールされたトリガーテーブルとデルタ・テーブルを使用して、後続のデルタ・マイグレーションを実行します。 その場合、ライブ Adobe Commerce 1 DB のコピーには、Data Migration Tool が移行の実行に使用するトリガーテーブルおよび差分テーブルは含まれません。

### 考えられる解決策

移行の問題を修正するには、Adobe Commerce 1 データベースのコピーから移行プロセスをテストすることをお勧めします。 コピーの問題を修正した後、ライブ Adobe Commerce 1 データベースから移行プロセスを再度開始します。 これにより、移行プロセスをスムーズにおこなうことができます。

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)

