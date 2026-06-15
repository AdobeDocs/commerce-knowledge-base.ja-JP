---
title: データ移行ツールのトラブルシューティング
description: この記事では、データ移行ツールの実行時に発生する可能性のあるエラーの解決策を提供します。
exl-id: 9beb31ae-ed3c-42e1-b0bf-33fb1c91e0ea
feature: Data Import/Export
role: Developer
source-git-commit: be0c72a1759ba172666c7c9409c65a1a388e3f11
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# データ移行ツールのトラブルシューティング

この記事では、データ移行ツールの実行時に発生する可能性のあるエラーの解決策を提供します。

## Source ドキュメント/フィールドがマッピングされていません {#source-documents-fields-not-mapped}

### エラーメッセージ

* `Source documents are not mapped: <EXTENSION_TABLE>`
* `Source fields are not mapped. Document: <EXTENSION_TABLE>. Fields: <EXTENSION_FIELD>`

まれに、メッセージに以下の項目が記載されることがあります

```bash
Destination documents
```

または

```bash
Destination fields
```

設定できます。

### 原因

一部のAdobe Commerce バージョン 1 エンティティ（ほとんどの場合、拡張機能から取得）は、Adobe Commerce バージョン 2 データベースに存在しません。

このメッセージは、Data Migration Toolが内部テストを実行して、テーブルとフィールドが&#x200B;*source* （Adobe Commerce 1）と&#x200B;*destination* （Adobe Commerce 2）のデータベース間で一貫性があることを確認するために表示されます。

### 可能な解決策

* 対応するAdobe Commerce 2拡張機能を[Commerce Marketplace](https://marketplace.magento.com/)からインストールします。     競合するデータが独自のデータベース構造要素を追加する拡張機能から発生している場合、同じ拡張機能のAdobe Commerce 2版は、そのような要素を宛先（Adobe Commerce 2）データベースに追加する可能性があり、問題を修正します。
* ツールの実行時に`-a`引数を使用して、エラーを自動解決し、移行が停止するのを防ぎます。
* 問題のあるデータを無視するようにツールを設定します。

データベースエンティティを無視するには、次のように、`map.xml` ファイルのエンティティに`<ignore>` タグを追加します。

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
>マップファイルまたは`-a` オプションを使用してエンティティを無視する前に、影響を受けるデータがAdobe Commerce 2 ストアに必要ないことを確認してください。

## クラスがレコードにマッピングされていません {#class-does-not-exist-but-mentioned}

### エラーメッセージ

```bash
Class <extension/class_name> is not mapped in record <attribute_id=196>
```

### 原因

Adobe Commerce 1 コードベースのクラスは、開発者向けドキュメントの[EAV移行手順](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/data-migration/basics/technical-specification)中にAdobe Commerce 2 コードベースで見つかりませんでした。 ほとんどの場合、欠落しているクラスは[拡張機能](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/glossary#extension)に属しています。

### 可能な解決策

* 対応するAdobe Commerce 2拡張機能をインストールします。
* 問題の原因となる属性を無視します。    このために、`eav-attribute-groups.xml.dist` ファイルの`ignore` グループに属性を追加します。
* `class-map.xml.dist` ファイルを使用してクラスマッピングを追加します。

## 外部キーの制約が失敗する

### エラーメッセージテキスト

```bash
Foreign key <KEY_NAME> constraint fails on source database. Orphan records id: <id_1>, <id_2> from <child_table>.<field_id> has no referenced records in <parent_table>
```

### 原因

`child_table`の`field_id`が指している`parent_table`にデータベース レコードがありません。

### 考えられる解決策

レコードが必要ない場合は、`child_table`からレコードを削除します。

レコードを保持するには、データ移行ツールの`config.xml`を変更して`Data Integrity Step`を無効にします。

## URL書き換えの重複

```xml
There are duplicates in URL rewrites:
Request path: towel.html Store ID: 2 Target path: catalog/product/view/id/10
Request path: towel.html Store ID: 2 Target path: catalog/product/view/id/12
```

### 原因

URL書き換え内の`Target path`は、`Request path` + `Store ID`の一意のペアで指定する必要があります。 このエラーは、同じ`Request path` + `Store ID` ペアを使用し、2つの異なる`Target path`値を持つ2つのエントリを報告します。

### 考えられる解決策

`config.xml` ファイルで`auto_resolve_urlrewrite_duplicates` オプションを有効にします。

この設定では、URL書き換えの競合レコードにハッシュ文字列を追加し、コマンドラインインターフェイスに解決結果を表示します。

## エンティティの不一致 {#mismatch-of-entities}

### エラーメッセージ

```bash
Mismatch of entities in the document: <DOCUMENT> Source: <COUNT_ITEMS_IN_SOURCE_TABLE> Destination: <COUNT_ITEMS_IN_DESTINATION_TABLE>
```

### 原因

このエラーは、ボリュームチェック手順の実行中に発生します。 つまり、ドキュメントのAdobe Commerce 2 データベースレコード数は、Adobe Commerce 1と同じではありません。

顧客が移行中に注文を行うと、欠落したレコードが発生します。

### 考えられる解決策

データ移行ツールを`Delta` モードで実行して、増分変更を転送します。

## Deltalogがインストールされていません {#deltalog-is-not-installed}

### エラーメッセージ

```bash
Deltalog for <TABLE_NAME> is not installed
```

### 原因

このエラーは、データへの変更の[増分移行](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/data-migration/migrate-data/delta) （開発者向けドキュメント）中に発生します。 つまり、（プレフィックス `m2_cl_*`を含む） deltalog テーブルがAdobe Commerce 1 データベースに見つかりませんでした。 これらのテーブルは、[data migration](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/data-migration/migrate-data/data) （開発者向けドキュメント）の間にインストールされます。また、変更を追跡してdeltalog テーブルを入力するデータベーストリガーもインストールされます。

このエラーの原因の1つは、ライブストア自体からではなく、ライブAdobe Commerce 1 ストアの&#x200B;*コピー*&#x200B;から移行しようとしていることです。 移行されていないライブ Adobe Commerce 1 ストアからコピーを作成する場合、コピーには差分移行を完了するために必要なトリガーと追加の差分テーブルが含まれていないため、移行は失敗します。 データ移行ツールは、違いを移行するためにAC1とAC2のDBを比較しません。 代わりに、最初の移行時にインストールされたトリガーとdeltalog テーブルを使用して、後続のdelta移行を実行します。 このような場合、ライブ Adobe Commerce 1 DBのコピーには、Data Migration Toolが移行を実行するために使用するトリガーとdeltalog テーブルは含まれません。

### 考えられる解決策

移行の問題を修正するために、Adobe Commerce 1 データベースのコピーから移行プロセスをテストすることをお勧めします。 コピーの問題を修正した後、ライブのAdobe Commerce 1 データベースから移行プロセスを再度開始します。 これにより、移行プロセスをスムーズに進めることができます。

## 関連トピックス

[Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)

