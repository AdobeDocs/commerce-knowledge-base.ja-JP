---
title: スケジュール更新の終了日を編集した後、カタログのルール テーブルのエントリが重複する
description: この記事では、Adobe Commerce 2.2.3 の既知の問題に対するパッチを提供します。カタログの価格ルール スケジュールの更新の終了日または時刻を変更すると、「catalogrule」テーブルに重複するエントリが追加され、「catalogrule_rule」（カタログルール商品）インデクサーのインデックスでエラーが発生します。
exl-id: e900b712-d0f5-4404-8441-64522035ce44
feature: Cache, Catalog Management, Marketing Tools
role: Developer
source-git-commit: 496151d1fe29a66d84349e4a96e7c5563a92c5c4
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---

# スケジュール更新の終了日を編集した後、カタログのルール テーブルのエントリが重複する

この記事では、Adobe Commerce 2.2.3 の既知の問題に対するパッチを提供しています。このパッチでは、カタログ価格ルールのスケジュール更新の終了日または時刻を変更すると、に重複するエントリが追加されます `catalogrule` テーブルとエラー `catalogrule_rule` （カタログルール製品）インデクサーの再インデックス。

## 問題

既存のカタログ価格ルールのスケジュール更新の終了日または時刻を変更すると、重複するエントリが `catalogrule` データベーステーブル。 その結果、 `catalogrule_rule` 再インデックスが失敗し、例外ログに次のエラーが記録されます。 *同じ ID の項目が既に存在しています*.

<u>再現手順</u>:

前提条件：次の `catalogrule_rule` インデクサーはに設定されています。 *[スケジュールに従って更新](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/indexer-configuration.html)* モード。

1. Commerce管理者で、の下に新しいカタログ価格ルールを作成します。 **Marketing** > **プロモーション** > **カタログ価格ルール**.
1. が含まれる **カタログ価格ルール** グリッド、クリック **編集**&#x200B;新しい更新をスケジュールして設定します **ステータス** 対象： *アクティブ。*
1. クリック **表示/編集** 新しく作成された更新の横で、終了日を以前の日付に変更します。
1. 更新を保存します。
1. の reindex コマンドを実行します。 `catalogrule_rule` インデクサー。

<u>期待される結果</u>:

この `catalogrule_rule` インデクサーのインデックスが正常に再作成されました。 には重複するエントリはありません `catalogrule` テーブル。

<u>実際の結果</u>:

再インデックスに失敗し、次のエラーが発生します。 *同じ ID の項目が既に存在しています*&#x200B;には重複するエントリがあるためです `catalogrule` テーブル。

## 解決策

この問題を解決するには、添付されているパッチを適用し、既存の重複エントリを削除する必要があります。 を参照してください。 [重複したエントリの削除](#remove) 重複が存在するかどうかの確認と削除について詳しくは、を参照してください。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-10974\_EE\_2.2.3\_COMPOSER\_v2.patch のダウンロード](assets/MDVA-10974_EE_2.2.3_COMPOSER_v2.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* Adobe Commerce 2.2.3

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.1 - 2.2.5
* Adobe Commerce オンプレミス 2.2.1 ～ 2.2.2 および 2.2.4 ～ 2.2.5

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 詳しくは、サポートナレッジベースを参照してください。

## 重複したエントリの削除 {#remove}

>[!NOTE]
>
>操作を行う前に、最新のバックアップを作成してください。

重複したエントリを探して削除するには、次の手順を実行します。

1. 次のクエリを実行して、重複したエントリがデータベース内に存在するかどうかを確認します。

   ```SQL
   SELECT entity_id, "catalog_product_entity" AS entity_table FROM catalog_product_entity GROUP BY entity_id, created_in HAVING COUNT(*) > 1    UNION    SELECT entity_id, "catalog_product_entity" AS entity_table FROM catalog_product_entity group by entity_id, updated_in having count(*) > 1    UNION    SELECT rule_id as entity_id, "catalogrule" AS entity_table FROM catalogrule GROUP BY entity_id, created_in HAVING COUNT(*) > 1    UNION    SELECT rule_id as entity_id, "catalogrule" AS entity_table FROM catalogrule GROUP BY entity_id, updated_in HAVING COUNT(*) > 1    UNION    SELECT rule_id as entity_id, "salesrule" AS entity_table FROM salesrule GROUP BY entity_id, created_in HAVING COUNT(*) > 1    UNION    SELECT rule_id as entity_id, "salesrule" AS entity_table FROM salesrule GROUP BY entity_id, updated_in HAVING COUNT(*) > 1    UNION    SELECT page_id as entity_id, "cms_page" AS entity_table FROM cms_page GROUP BY entity_id, created_in HAVING COUNT(*) > 1    UNION    SELECT page_id as entity_id, "cms_page" AS entity_table FROM cms_page GROUP BY entity_id, updated_in HAVING COUNT(*) > 1    UNION    SELECT block_id as entity_id, "cms_block" AS entity_table FROM cms_block GROUP BY entity_id, created_in HAVING COUNT(*) > 1    UNION    SELECT block_id as entity_id, "cms_block" AS entity_table FROM cms_block GROUP BY entity_id, updated_in HAVING COUNT(*) > 1;
   ```

   重複するエントリがない場合、応答は空になり、それ以外の操作は必要ありません。 重複したエントリが存在する場合は、テーブル名と `entity_id` （次の例に示すような複製されたエンティティ）。

   ![table_results1.png](assets/table_results1.png)

   特定のテーブルでは、エンティティ ID を持つフィールドの名前は次の名前とは異なることに注意してください `entity_id`. 例： `cms_page` テーブル、のようになります `page_id` の代わりに `entity_id`.

1. 次に、重複について詳しく見ていき、どちらを削除する必要があるかを理解する必要があります。 次のようなクエリを使用して、重複を確認します。 前の手順で受け取った結果に従って、テーブル名、エンティティ ID 名、値を置き換えます。

   ```sql
   SELECT row_id, entity_id, created_in, updated_in FROM catalog_product_entity WHERE entity_id = 483 ORDER BY created_in;
   ```

   複数の列を持つレコードのリストが表示されます。 例：

   ![table_results2.png](assets/table_results2.png)

   この `created_in` および `updated_in` 値は、次のパターンに従う必要があります。 `created_in` 現在の行の値は次と等しい `updated_in` 前の行の値。 また、 **最初の行** created\_in = 1 と **最後の行** updated\_in = 2147483647 が含まれている必要があります。 （行が 1 つしかない場合は、created\_in=1 と表示されます。 **および** 更新されました\_in=2147483647）。 このパターンが適用されていない行を削除する必要があります。 この例では、次を含む行になります `row_id` =2052 （2 行目と 3 行目の両方で created_in: 1540837826 の値が同じであるため、この値は発生しません。

1. 次のようなクエリを使用して、重複を削除します。 前の手順で受け取った結果に従って、テーブル名、エンティティ ID 名、値を置き換えます。

   ```sql
   DELETE FROM catalog_product_entity WHERE entity_id = 483 AND row_id = 2052;
   ```

1. 次を実行してキャッシュをクリーンアップします。

   ```bash
   bin/magento cache:clean
   ```

   または、の下のCommerce管理で確認できます。 **システム** > **ツール** > **キャッシュ管理**.

## 開発者向けドキュメントの便利なリンク

* [クラウドインフラストラクチャー上のAdobe Commerceにカスタムパッチを適用](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)
* [クラウドインフラストラクチャー上のAdobe Commerceのログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)）

## 添付ファイル
