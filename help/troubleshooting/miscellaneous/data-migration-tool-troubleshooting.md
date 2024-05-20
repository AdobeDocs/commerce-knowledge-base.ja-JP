---
title: データ移行ツールのトラブルシューティング
description: この記事では、データ移行ツールの実行時に発生する可能性のあるエラーの解決策について説明します。
exl-id: 9beb31ae-ed3c-42e1-b0bf-33fb1c91e0ea
feature: Data Import/Export
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# データ移行ツールのトラブルシューティング

この記事では、データ移行ツールの実行時に発生する可能性のあるエラーの解決策について説明します。

## マッピングされていないソースドキュメント/フィールド {#source-documents-fields-not-mapped}

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

このメッセージが表示されるのは、データ移行ツールが内部テストを実行して、テーブルとフィールドが間で一致していることを確認するからです *ソース* （Adobe Commerce 1）と *宛先* （Adobe Commerce 2）データベース。

### 可能な解決策

* 対応するAdobe Commerce 2 拡張機能をからインストールします。 [Commerce Marketplace](https://marketplace.magento.com/).     競合するデータの発行元が独自のデータベース構造要素を追加する拡張機能の場合、同じ拡張機能のAdobe Commerce 2 バージョンは、対象の（Adobe Commerce 2） データベースにこのような要素を追加し、問題を解決する可能性があります。
* の使用 `-a` エラーを自動解決し、移行が停止するのを防ぐためのツール実行時の引数。
* 問題のあるデータを無視するようにツールを設定します。

データベースエンティティを無視するには、 `<ignore>` でエンティティにタグ付け `map.xml` ファイル。例：

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
>マップファイルを使用してエンティティを無視する前、または `-a` オプションとして、影響を受けるデータをAdobe Commerce 2 ストアで必要としていないことを確認します。

## クラスがレコードにマッピングされていません {#class-does-not-exist-but-mentioned}

### エラーメッセージ

```bash
Class <extension/class_name> is not mapped in record <attribute_id=196>
```

### 原因：

の間、Adobe Commerce 1 コードベースのクラスがAdobe Commerce 2 コードベースに見つかりませんでした [EAV 移行手順](https://devdocs.magento.com/guides/v2.3/migration/migration-tool-internal-spec.html#eav) 開発者向けドキュメントを参照してください。 ほとんどの場合、不足しているクラスは [拡張子](https://glossary.magento.com/extension).

### 可能な解決策

* 対応するAdobe Commerce 2 拡張機能をインストールします。
* 問題の原因となった属性を無視します。    この場合、属性をに追加します `ignore` グループの検索条件 `eav-attribute-groups.xml.dist` ファイル。
* を使用したクラスマッピングの追加 `class-map.xml.dist` ファイル。

## 外部キー制約に失敗します

### エラーメッセージのテキスト

```bash
Foreign key <KEY_NAME> constraint fails on source database. Orphan records id: <id_1>, <id_2> from <child_table>.<field_id> has no referenced records in <parent_table>
```

### 原因：

にデータベースレコードがありません `parent_table` に対する `field_id` の `child_table` はを指しています。

### 考えられる解決策

からのレコードの削除 `child_table` 必要ない場合は、

レコードを保持するには、を無効にします `Data Integrity Step` データ移行ツールの `config.xml` .

## URL リライトの重複

```xml
There are duplicates in URL rewrites:
Request path: towel.html Store ID: 2 Target path: catalog/product/view/id/10
Request path: towel.html Store ID: 2 Target path: catalog/product/view/id/12
```

### 原因：

この `Target path` url 書き換えでは、次の一意のペアで指定する必要があります `Request path` + `Store ID` . このエラーは、同じを使用する 2 つのエントリを報告します `Request path` + `Store ID` 2 つの異なるペア `Target path` 値。

### 考えられる解決策

を有効にする `auto_resolve_urlrewrite_duplicates` のオプション `config.xml` ファイル。

この設定により、の競合するレコードにハッシュ文字列が追加されます。 [URL](https://glossary.magento.com/url) コマンドラインインターフェイスに書き換えて、解像度の結果を表示します。

## エンティティの不一致 {#mismatch-of-entities}

### エラーメッセージ

```bash
Mismatch of entities in the document: <DOCUMENT> Source: <COUNT_ITEMS_IN_SOURCE_TABLE> Destination: <COUNT_ITEMS_IN_DESTINATION_TABLE>
```

### 原因：

エラーは、ボリュームチェックの手順で発生。 つまり、ドキュメントのAdobe Commerce 2 データベースレコード数は、Adobe Commerce 1 と同じではありません。

レコードの欠落は、顧客が移行中に注文を行った場合に発生します。

### 考えられる解決策

でデータ移行ツールを実行する `Delta` 増分の変更を転送するモード。

## Deltalog がインストールされていません {#deltalog-is-not-installed}

### エラーメッセージ

```bash
Deltalog for <TABLE_NAME> is not installed
```

### 原因：

このエラーは次の場合に発生します [増分移行](https://devdocs.magento.com/guides/v2.3/migration/migration-migrate-delta.html) （開発者向けドキュメントの） データの変更。 これは、テーブルを削除することを意味します（プレフィックス付き） `m2_cl_*`）がAdobe Commerce 1 データベースに見つかりませんでした。 ツールは、次の期間にこれらのテーブルをインストールします [データ移行](https://devdocs.magento.com/guides/v2.3/migration/migration-migrate-data.html) （開発者向けドキュメントを参照）と、変更内容を追跡して差分テーブルに入力するデータベーストリガー。

エラーの理由の 1 つは、から移行しようとしていることです。 *コピー* ライブストア自体からではなく、ライブのAdobe Commerce 1 ストアの。 一度も移行されていないライブ Adobe Commerce 1 ストアからコピーを作成すると、そのコピーには、差分マイグレーションを行うのに必要なトリガーや追加の差分テーブルが含まれないので、マイグレーションが失敗します。 データ移行ツールでは、AC1 と AC2 の DB を比較して相違点を移行しません。 代わりに、最初のマイグレーション時にインストールされたトリガーテーブルとデルタ・テーブルを使用して、後続のデルタ・マイグレーションを実行します。 その場合、ライブ Adobe Commerce 1 DB のコピーには、Data Migration Tool が移行の実行に使用するトリガーテーブルおよび差分テーブルは含まれません。

### 考えられる解決策

移行の問題を修正するには、Adobe Commerce 1 データベースのコピーから移行プロセスをテストすることをお勧めします。 コピーの問題を修正した後、ライブ Adobe Commerce 1 データベースから移行プロセスを再度開始します。 これにより、移行プロセスをスムーズにおこなうことができます。
