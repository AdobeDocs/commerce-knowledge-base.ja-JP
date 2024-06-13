---
title: 処理に時間のかかるクエリの確認と MySQL の処理
description: この記事では、マーチャントのサイトに悪影響を与える可能性のある一般的な MySQL の問題（低速クエリ、時間がかかりすぎるプロセス）と、それらが示すソリューションについて説明します。
exl-id: cae02e4f-d8cb-4074-abac-24ead22bdc07
feature: Services
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 処理に時間のかかるクエリの確認と MySQL の処理

この記事では、マーチャントのサイトに悪影響を与える可能性のある一般的な MySQL の問題（低速クエリ、時間がかかりすぎるプロセス）と、それらが示すソリューションについて説明します。

## MySQL の「低速クエリ」を確認する

### 説明

データベースの過負荷が原因で停止が発生した場合は、次の手順を実行すると、データベースの低速クエリログを確認するのに役立ちます。

### MySQL コマンドラインを使用したクエリの分析（Adobe Commerce Cloud/オンプレミス/Magento Open Source）

1. MySQL コマンドライン（Adobe Commerce オンプレミス/Magento Open Source）またはコマンドライン（クラウドインフラストラクチャー上のAdobe Commerce）からクラウドサーバーにログインします。
1. 低速のクエリログで、50 秒を超えるクエリを調べます。

   ```bash
   grep 'Query_time: [5-9][0-9]\|Query_time: [0-9][0-9][0-9]' /var/log/mysql/mysql-slow.log -A 3
   ```

1. に移動 <https://www.unixtimestamp.com/> （または同様の Unix タイムスタンプコンバーター）を使用して、処理に時間のかかるクエリが実行されたときのタイムスタンプを挿入します。
1. 発生したサイトの停止に関連する時間がある場合は、データベースの過負荷が原因である可能性があります。 その時点でデータベースにどのような負荷がかかっていたかを確認します。 このような負荷の例を次に示します。

* Cron プロセス
* トラフィック（ボットまたは人物）
* インポート/エクスポート スクリプト
* ダンプの作成


### を使用したクエリの分析 [!DNL Percona Toolkit] （Adobe Commerce Pro：クラウドアーキテクチャのみ）

Adobe Commerce プロジェクトが Pro アーキテクチャにデプロイされている場合は、 [!DNL Percona Toolkit] クエリを分析します。

1. を実行 `pt-query-digest --type=slowlog` mysql の低速なクエリログに対してコマンドを実行します。
   * 処理に時間のかかるクエリログの場所については、を参照してください。 **[[!UICONTROL Log locations > Service Logs]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)** 開発者向けドキュメントを参照してください。
   * を参照してください。 [[!DNL Percona Toolkit] > pt-query-digest](https://www.percona.com/doc/percona-toolkit/LATEST/pt-query-digest.html#pt-query-digest) ドキュメント。
1. 見つかった問題に基づいて、クエリを修正する手順を実行して、クエリをより迅速に実行します。

## MySQL の「プロセスリスト」を確認しています

### 説明

これにより、MySQL サーバーが稼働しているかどうか、また、スタックしたクエリがないかどうかを確認できます。

### 手順

1. MySQL コマンドライン（Adobe Commerce オンプレミス/Magento Open Source）またはコマンドライン（クラウドインフラストラクチャー上のAdobe Commerce）からクラウドサーバーにログインします。
1. 以下のコードのブロックを使用して MySQL にログインします。 これにより、ログインのプロセスが自動化されます。

   ```MySQL
   `export DB_NAME=$(grep [\']db[\'] -A 20 app/etc/env.php | grep dbname | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/['][,]//");    export MYSQL_HOST=$(grep [\']db[\'] -A 20 app/etc/env.php | grep host | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/['][,]//");    export DB_USER=$(grep [\']db[\'] -A 20 app/etc/env.php | grep username | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/['][,]//");    export MYSQL_PWD=$(grep [\']db[\'] -A 20 app/etc/env.php | grep password | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/[']$//" | sed "s/['][,]//");    mysql -h $MYSQL_HOST -u $DB_USER --password=$MYSQL_PWD $DB_NAME -U -A -e 'show processlist;`
   ```

1. エラーが戻ったり、応答に 30 秒以上かかる場合は、サポートに連絡して MySQL サーバーを確認してください。
1. サンプル出力を確認します。

1. 次に、出力例を示します。

   ```MySQL
   `$ mysql -h $MYSQL_HOST -u $DB_USER --password=$MYSQL_PWD $DB_NAME -U -A -e 'show processlist;'    +-----------+---------------+--------------------+---------------+---------+------+----------------+------------------------------------------------------------------------------------------------------+----------+    | Id        | User          | Host               | db            | Command | Time | State          | Info                                                                                                 | Progress |    +-----------+---------------+--------------------+---------------+---------+------+----------------+------------------------------------------------------------------------------------------------------+----------+    | 123456789 | abcdefghijklm | 192.168.7.10:12345 | abcdefghijklm | Query   |    0 | Writing to net | SELECT `magento_versionscms_hierarchy_node`.*, `page_table`.`title` AS `page_title`, `page_table`.`i |    0.000 |    | 123456788 | abcdefghijklm | 192.168.7.10:12344 | abcdefghijklm | Sleep   |    0 |                | NULL                                                                                                 |    0.000 |    | 123456777 | abcdefghijklm | 192.168.7.10:12333 | abcdefghijklm | Sleep   |    0 |                | NULL                                                                                                 |    0.000 |    | 123456666 | abcdefghijklm | 192.168.5.8:12222  | abcdefghijklm | Sleep   |    0 |                | NULL                                                                                                 |    0.000 |`
   ```

1. 「時間」列をチェックして、1800 秒を超える時間を確認します。これは、完了するのに時間がかかりすぎる可能性があるプロセスを示します。 「状態」列のプロセスのステータスに注意してください。
1. クエリを確認し、その期間の実行が予想されない場合はクエリを強制終了する可能性があります。 長時間実行されているクエリが予想される場合があります。


## 関連資料

* [MySQL Show Processlist 構文](https://dev.mysql.com/doc/refman/8.0/en/show-processlist.html) （dev.mysql.com内）。
* [MySQL Kill 構文](https://dev.mysql.com/doc/refman/8.0/en/kill.html) （dev.mysql.com内）。
* [セキュリティ、パフォーマンス、データ処理](https://devdocs.magento.com/guides/v2.3/ext-best-practices/extension-coding/security-performance-data-bp.html) 開発者向けドキュメントを参照してください。
* [MySQL ヘルプ](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/mysql.html) 開発者向けドキュメントを参照してください。
