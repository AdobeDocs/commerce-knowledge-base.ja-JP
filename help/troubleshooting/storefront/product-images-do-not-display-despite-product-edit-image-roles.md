---
title: 製品編集画像の役割にもかかわらず、製品画像が表示されない
description: この記事では、製品の編集ページで画像の役割が設定されているにもかかわらず、製品画像がストアフロントに表示されない場合の解決策について説明します。
exl-id: 456baa5a-fa16-4bc1-9d6c-54106fae58ca
feature: Cache, Products, Roles/Permissions, Storefront
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# 製品編集画像の役割にもかかわらず、製品画像が表示されない

この記事では、製品の編集ページで画像の役割が設定されているにもかかわらず、製品画像がストアフロントに表示されない場合の解決策について説明します。

**原因：** 複数のストアを持つAdobe Commerce インスタンスでは、一部の商品画像に `no_selection` 画像の役割属性の値 `image`, `small_image`, `thumbnail`, `swatch`. その `no_selection` 値が出現するのは、製品イメージの役割が、特定のストアのスコープ（つまり、 **すべてのストア表示** 特定のものの代わりに **ストア表示**）に設定します。 これがあなたのケースかどうかを理解するには、から SQL スクリプトを実行します **原因：** セクションを下にします。

**解決策：** を使用して行を削除 `no_selection` 以下の「解決策」セクションの SQL スクリプトを使用して、このような画像の値を指定します。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス 2.X.X
* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce

## 問題

管理パネルの製品ページで画像の役割（ベース、小、サムネール、スウォッチ）が正しく設定されていても、製品画像がストアフロントに表示されない場合があります。

製品ページを次のように確認した場合 **ストア表示** をに設定 **すべてのストア表示**&#x200B;の役割が設定されています。 **画像の詳細** 画面。

![all_store_views.png](assets/all_store_views.png)

![image_roles.png](assets/image_roles.png)

ただし、ストアフロントでは画像が表示されません。特定のストアレベルで製品ページを確認する場合（ **ストア表示**）を選択します。画像は表示されますが、役割が設定されていません。

![image_roles_not_set.png](assets/image_roles_not_set.png)

## 原因：

（複数のストアを持つ）マルチストアAdobe Commerceインスタンスでは、一部の商品画像に次の記号が表示されることがあります `no_selection` 属性値 `image`, `small_image`, `thumbnail`, `swatch` （これらの属性は画像の役割に対応します）。 その `no_selection` 値が出現するのは、製品イメージの役割が、特定のストアのスコープ（つまり、 **すべてのストア表示** 特定のものの代わりに **ストア表示**）に設定します。

技術的には、次の通りです。 `store_id=0` （Adobe Commerce インスタンス上のすべてのストアに対するグローバル設定を保持します）。product image roles が設定されている場合もあります。つまり、次の属性があります。 `image`, `small_image`, `thumbnail`, `swatch` 有効な値（画像へのパス）がある。 同時に、 `store_id=1` （特定のストア表現です）。これらの属性の値は次のとおりです `no_selection`.

### これが問題であることを確認する方法

次の SQL クエリを実行します。

```sql
SELECT `cpev_s`.*, `cpev_0`.`value` AS `store_value` FROM `catalog_product_entity_varchar` `cpev_s` JOIN `eav_attribute` `ea` ON `cpev_s`.`attribute_id` = `ea`.`attribute_id` LEFT JOIN `catalog_product_entity_varchar` `cpev_0` ON `cpev_0`.`row_id` = `cpev_s`.`row_id` AND `cpev_0`.`attribute_id` = `cpev_s`.`attribute_id` AND `cpev_0`.`store_id` = 0 WHERE `cpev_s`.`value` = 'no_selection' AND `ea`.`attribute_code` IN ('image', 'small_image', 'thumbnail') AND `cpev_s`.`store_id` > 0 AND `cpev_s`.`value` != `cpev_0`.`value` AND `cpev_s`.`value` = 'no_selection';
```

クエリが次のような結果を返す場合は、この記事に記載されている問題を処理しています。

```sql
+----------+--------------+----------+--------+--------------+----------------------------+
| value_id | attribute_id | store_id | row_id | value        | store_value                |
+----------+--------------+----------+--------+--------------+----------------------------+
|    67722 |           87 |        1 |    481 | no_selection | /3/5/355sss1_main.jpg      |
|    67723 |           88 |        1 |    481 | no_selection | /3/5/355sss1_main.jpg      |
|    67724 |           89 |        1 |    481 | no_selection | /3/5/355sss1_main.jpg      |
|    67814 |           87 |        1 |    503 | no_selection | /s/k/skb2031_main.jpg      |
|     6769 |           87 |        2 |    503 | no_selection | /s/k/skb2031_main.jpg      |
|    67815 |           88 |        1 |    503 | no_selection | /s/k/skb2031_main.jpg      |
|     6770 |           88 |        2 |    503 | no_selection | /s/k/skb2031_main.jpg      |
|    67816 |           89 |        1 |    503 | no_selection | /s/k/skb2031_main.jpg      |
|     6771 |           89 |        2 |    503 | no_selection | /s/k/skb2031_main.jpg      |
+----------+--------------+----------+--------+--------------+----------------------------+
9 rows in set (0.06 sec)
```

### なぜこれが起こるのですか？

Adobe Commerce アプリケーションに複数のストアがある場合、特定のストアとグローバルストア設定の間でデータが同期されない場合があります。

の値 `store_id=1` デフォルト（グローバル）ストア（`store_id=0`）に設定します。 したがって、アプリケーションはグローバル画像設定を無視して、ストアスコープ設定（`no_selection` （画像の役割の属性の場合）。画像を表示する場合に選択します。

## 解決策 {#solution}

を使用して属性を削除する `no_selection` この SQL スクリプトを使用する値：

```
DELETE `cpev_s`.* FROM `catalog_product_entity_varchar` `cpev_s` JOIN `eav_attribute` `ea` ON `cpev_s`.`attribute_id` = `ea`.`attribute_id` LEFT JOIN `catalog_product_entity_varchar` `cpev_0` ON `cpev_0`.`row_id` = `cpev_s`.`row_id` AND `cpev_0`.`attribute_id` = `cpev_s`.`attribute_id` AND `cpev_0`.`store_id` = 0 WHERE `cpev_s`.`value` = 'no_selection' AND `ea`.`attribute_code` IN ('image', 'small_image', 'thumbnail') AND `cpev_s`.`store_id` > 0 AND `cpev_s`.`value` != `cpev_0`.`value` AND `cpev_s`.`value` = 'no_selection';
```

これらの属性が削除されると、特定のストアの役割が設定され、ストアフロントに画像が表示されます。

## 追加の詳細

Adobe Commerce インスタンスでフルページキャッシュが有効になっている場合、すぐに修正結果を確認することはできません。

変更を表示するには、次を使用してページキャッシュを更新します。 **キャッシュ管理** 管理パネルのメニュー。

## 詳細情報

### ストアと範囲

[ストアとストアの範囲](/docs/commerce-admin/stores-sales/site-store/stores.html) ユーザーガイドの

### 画像

[製品画像のアップロード](/docs/commerce-admin/catalog/products/digital-assets/product-image.html#upload-an-image) ユーザーガイドの

### キャッシュ

* [キャッシュ管理](/docs/commerce-admin/systems/tools/cache-management.html) （ユーザー管理システムガイド）を参照してください。
* [キャッシュの管理](/docs/commerce-operations/configuration-guide/cli/manage-cache.html) 開発者向けドキュメントで