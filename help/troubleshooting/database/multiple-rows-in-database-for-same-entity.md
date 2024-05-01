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

ここで、 `$entityID = ID` カテゴリ /製品/ カート価格ルール / カタログ価格ルール / CMS ページの。

| Entity | $entityTable | 列（$C） |
|------------------|-----------------------------------|------------------|
| カテゴリ/製品 | catalog_category_entity/catalog_product_entity | entity_id |
| 買い物かご価格ルール/カタログ価格ルール | salesrule/catalogrule | rule_id |
| CMS ページ | cms_page | page_id |

## 原因：

これは想定されている動作です。 コンテンツのステージング機能によって、複数の行が作成されます。

* 終了日を指定せずに開始日を指定した場合、同じエンティティ/ルール/ページ ID を持つ行が少なくとも 2 つ存在します。 1 つの行は、エンティティの元の状態を示します（の行） `created_in=1`）を選択します。1 つの行は、を示します *スケジュールされた更新の終了*.

* 開始日と終了日を指定した場合、同じエンティティ/ルール/ページ ID を持つ行が少なくとも 3 つ存在することになります。 1 つの行は、エンティティの元の状態を示します（の行） `created_in=1`）、1 つの行はに対応します *スケジュールされた更新の開始*&#x200B;を選択すると、1 行がに設定されます *スケジュールされた更新の終了*.

例えば、次のクエリの場合：

```
SELECT row_id, entity_id, created_in, updated_in FROM catalog_product_entity WHERE entity_id = 483 ORDER BY created_in;
```

![multiple_rows_in_database.png](assets/multiple_rows_in_database.png)

* この `created_in` および `updated_in` 値は、次のパターンに従う必要があります：は `created_in` 現在の行の値は次と等しい `updated_in` 前の行の値。 また、最初の行にはを含める必要があります `created_in = 1` 最後の行にはが含まれます `updated_in = 2147483647`. （行が 1 つしかない場合は、次を確認する必要があります `created_in=1` および `updated_in=2147483647`）に設定します。

### 2 つ目の DB エントリ（および次のエントリすべて）が同じエンティティの DB に表示されるのはなぜですか？

* 影響を受けるエンティティの 2 つ目の DB レコード（場合によっては次のレコード）は、を使用してコンテンツステージングの更新がスケジュールされていることを意味します `Magento_Staging` 各テーブル内のエンティティに対して追加のレコードを作成するモジュール。

問題は、レコードの値がと同じ場合にのみ発生します。 `created_in` または `updated_in` 列。

## 解決策

これは想定されている動作で、行間に不一致がある場合にのみ問題が発生します。

## 関連資料

* [カテゴリへの変更が保存されない](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/changes-to-categories-are-not-being-saved.html) サポートナレッジベースで。
* [スケジュール更新の終了日を編集した後、カタログのルール テーブルのエントリが重複する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/duplicate-entries-in-the-catalogrule-table-after-editing-the-end-date-of-a-schedule-update.html) サポートナレッジベースで。
