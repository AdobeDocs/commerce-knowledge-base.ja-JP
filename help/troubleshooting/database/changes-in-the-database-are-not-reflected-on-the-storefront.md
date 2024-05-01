---
title: データベースの変更は、ストアフロントには反映されません
description: この記事では、適用されるエンティティ更新の遅延や中断を回避するためのソリューションを提供します。 これには、変更ログテーブルのサイズが大きくなりすぎるのを防ぐ方法や、MySQL テーブルのトリガーを設定する方法が含まれます。
exl-id: ac52c808-299f-4d08-902f-f87db1fa7ca6
feature: Catalog Management, Categories, Services, Storefront
role: Developer
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# データベースの変更は、ストアフロントには反映されません

この記事では、適用されるエンティティ更新の遅延や中断を回避するためのソリューションを提供します。 これには、変更ログテーブルのサイズが大きくなりすぎるのを防ぐ方法や、MySQL テーブルのトリガーを設定する方法が含まれます。

影響を受ける製品とバージョン：

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Adobe Commerce オンプレミス 2.2.x、2.3.x

## 問題

データベースで加えた変更がストアフロントに反映されないか、エンティティの更新の適用に大きな遅延があります。 影響を受ける可能性のあるエンティティには、製品、カテゴリ、価格、在庫、カタログルール、販売ルール、ターゲットルールが含まれます。

## 原因：

インデクサーが [スケジュールに従って更新するように設定](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-index.html#configure-indexers)この問題は、変更ログが大きすぎる、または MySQL トリガーが設定されていない 1 つ以上のテーブルが原因である可能性があります。

### 変更ログテーブルのサイズ超過

変更ログテーブルは、 `indexer_update_all_views` cron ジョブが複数回正常に完了しません。

変更ログテーブルは、エンティティに対する変更が追跡されるデータベーステーブルです。 変更が適用されない限り、レコードは変更ログテーブルに保存されます。変更が適用されるのは、 `indexer_update_all_views` cron ジョブ。 Adobe Commerce データベースには複数の変更ログテーブルがあり、INDEXER\_TABLE\_NAME + &#39;\_cl&#39;というパターンに従って名前が付けられています。例： `catalog_category_product_cl`, `catalog_product_category_cl`. データベースでの変更の追跡方法の詳細については、次を参照してください [インデックス作成の概要/Mview](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/indexing.html#m2devgde-mview) 開発者向けドキュメントの記事。

### MySQL データベーストリガーが設定されていない

エンティティ（product、category、target rule など）を追加または変更した後で、対応する変更ログ・テーブルにレコードが追加されていない場合、データベース・トリガーが設定されていないことが疑われます。

## 解決策

>[!WARNING]
>
>操作を実行する前にデータベースバックアップを作成し、サイトの負荷が高い期間は避けることを強くお勧めします。

### 変更ログテーブルのサイズが超過するのを防ぐ

必ずを `indexer_update_all_views` cron ジョブは常に正常に完了する。

次の SQL クエリを使用すると、の失敗したすべてのインスタンスを取得できます `indexer_update_all_views` cron ジョブ :

```sql
select * from cron_schedule where job_code = "indexer_update_all_views" and status
  <> "success" and status <> "pending";
```

または、以下を検索して、ログでそのステータスを確認できます。 `indexer_update_all_views` エントリ：

* `<install_directory>/var/log/cron.log` - バージョン 2.3.1 以降および 2.2.8 以降
* `<install_directory>/var/log/system.log`  – 以前のバージョン

### MySQL テーブルトリガーを再設定

不足している MySQL テーブルトリガーを設定するには、インデクサーモードを再設定する必要があります。

1. 「保存時」に切り替えます。
1. 「スケジュール通り」に戻します。

次のコマンドを使用して、この操作を実行します。

>[!WARNING]
>
>インデクサーモードを切り替える前に、web サイトを次の場所に配置することをお勧めします。 [整備](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#maintenance-mode) モードと [cron ジョブの無効化](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html#disable-cron-jobs) データベースのロックを回避します。

```bash
php bin/magento indexer:set-mode {realtime|schedule} [indexerName]
```

>[!INFO]
>
>インデクサー関連のデータベーストリガーは、インデクサーモードがスケジュールに設定されている場合は追加され、インデクサーモードがリアルタイムに設定されている場合は削除されます。 インデクサーがスケジュールに設定されている間にトリガーがデータベースにない場合は、インデクサーをリアルタイムに変更してから、スケジュールに戻します。 これにより、トリガーがリセットされます。

## 関連資料

<ul><li title="MySQL テーブルが大きすぎます"><a href="/help/troubleshooting/database/mysql-tables-are-too-large.md">MySQL テーブルが大きすぎます</a> サポートナレッジベースで。</li>
<li title="MySQL テーブルが大きすぎます"><a href="https://devdocs.magento.com/guides/v2.3/extension-dev-guide/indexing.html#m2devgde-mview">インデクサーの概要/Mview</a> 開発者向けドキュメントを参照してください。</li></ul>
