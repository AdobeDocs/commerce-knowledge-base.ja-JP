---
title: 同じエンティティの行がデータベース内に複数あります
description: この記事では、データベース内の同じエンティティ ID に対して複数の行が存在する問題の解決策を提供します。
feature: Catalog Management, Categories, Services, Storefront
role: Developer
exl-id: 09d5c321-9c45-4041-b6f6-831efca0977e
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 同じエンティティのデータベース内の複数の行

この記事では、データベース内の同じエンティティ ID に対して複数の行が存在する問題の解決策を提供します。

## 影響を受ける製品とバージョン：

* Adobe Commerce（すべてのバージョン）

## 問題

データベース内に同じエンティティ ID の行が複数あります。

例えば、エンティティ ID が重複するレコードのリストを受け取った後に、次のクエリを実行します。

```
SELECT * FROM $entityTable WHERE $column = <$entityID> ORDER BY created_in;
```

カテゴリ/製品/買い物かご価格ルール/カタログ価格ルール/CMS ページの `$entityID = ID`。

| Entity | $entityTable | 列（$C） |
|------------------|-----------------------------------|------------------|
| カテゴリ/製品 | catalog_category_entity/catalog_product_entity | entity_id |
| 買い物かご価格ルール/カタログ価格ルール | salesrule/catalogrule | rule_id |
| CMS ページ | cms_page | page_id |

## 原因：

これは想定されている動作です。 コンテンツのステージング機能によって、複数の行が作成されます。

* 終了日を指定せずに開始日を指定した場合、同じエンティティ/ルール/ページ ID を持つ行が少なくとも 2 つ存在します。 1 つの行はエンティティの元の状態（`created_in=1` の行）を示し、1 つの行は *スケジュールされた更新の終了* を示します。

* 開始日と終了日を指定した場合、同じエンティティ/ルール/ページ ID を持つ行が少なくとも 3 つ存在することになります。 1 つの行はエンティティの元の状態（`created_in=1` の行）、1 つの行は *予定更新の開始*、1 つの行は *予定更新の終了* を示します。

例えば、次のクエリの場合：

```
SELECT row_id, entity_id, created_in, updated_in FROM catalog_product_entity WHERE entity_id = 483 ORDER BY created_in;
```

![multiple_rows_in_database.png](assets/multiple_rows_in_database.png)

* `created_in` と `updated_in` の値は、次のパターンに従う必要があります。現在の行の `created_in` 値は、前の行の `updated_in` 値と等しくなります。 また、最初の行には `created_in = 1` を、最後の行には `updated_in = 2147483647` を含める必要があります。 （行が 1 つしかない場合は、`created_in=1` と `updated_in=2147483647` が表示されます）。

### 2 つ目の DB エントリ（および次のエントリすべて）が同じエンティティの DB に表示されるのはなぜですか？

* 影響を受けるエンティティの 2 つ目の DB レコード（場合によっては次のレコード）は、`Magento_Staging` モジュールを使用してコンテンツステージングの更新がスケジュールされていることを意味します。これにより、各テーブルのエンティティに対して追加のレコードが作成されます。

問題は、レコードの `created_in` 列または `updated_in` 列の値が同じ場合にのみ発生します。

## 解決策

これは想定されている動作で、行間に不一致がある場合にのみ問題が発生します。

## 関連資料

* [ カテゴリに対する変更は保存されません ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/changes-to-categories-are-not-being-saved.html) が、サポートナレッジベースに表示されます。
* [ スケジュール更新の終了日を編集した後、カタログルールテーブルのエントリを複製 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/duplicate-entries-in-the-catalogrule-table-after-editing-the-end-date-of-a-schedule-update.html) ます。サポートナレッジベースを参照してください。
