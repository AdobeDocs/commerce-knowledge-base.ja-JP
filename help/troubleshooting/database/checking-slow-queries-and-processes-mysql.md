---
title: MySQLの低速なクエリとプロセスを確認する
description: この記事では、マーチャントのサイトと示すソリューションに悪影響を及ぼす可能性のある、いくつかの一般的なMySQLの問題（クエリが遅い、プロセスが長すぎる）について説明します。
exl-id: cae02e4f-d8cb-4074-abac-24ead22bdc07
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
source-wordcount: '547'
ht-degree: 0%
---
# MySQLの低速なクエリとプロセスを確認する

この記事では、マーチャントのサイトと示すソリューションに悪影響を及ぼす可能性のある、いくつかの一般的なMySQLの問題（クエリが遅い、プロセスが長すぎる）について説明します。

## MySQLの「スロークエリ」の確認

### 説明

データベースの過負荷が原因の可能性がある障害が発生した場合は、次の手順を実行すると、データベースの低速クエリログを確認できます。

### MySQL コマンドラインを使用してクエリを分析する（Adobe Commerce Cloud/オンプレミス/Magento Open Source）

1. MySQL コマンドライン（Adobe Commerce オンプレミス/Magento Open Source）またはコマンドライン（Adobe Commerce オンクラウドインフラストラクチャ）からクラウドサーバーにログインします。
1. 50秒を超えるクエリの低速クエリログを調べます。

   ```bash
   grep 'Query_time: [5-9][0-9]\|Query_time: [0-9][0-9][0-9]' /var/log/mysql/mysql-slow.log -A 3
   ```

1. <https://www.unixtimestamp.com/> （または同様のUnix タイムスタンプコンバーター）に移動し、スロークエリが実行されたときのタイムスタンプを挿入します。
1. サイトの障害と時間が相関関係がある場合は、データベースの過負荷が原因である可能性があります。 その時点でデータベース上にどのような負荷があったかを確認します。 そのような負荷の例としては、次のものがあります。

* Cron プロセス
* トラフィック（ボットまたは人物）
* スクリプトの読み込み/書き出し
* ダンプの作成


### [!DNL Percona Toolkit]を使用してクエリを分析する（Adobe Commerce Pro: クラウドアーキテクチャのみ）

Adobe Commerce プロジェクトがPro アーキテクチャにデプロイされている場合は、[!DNL Percona Toolkit]を使用してクエリを分析できます。

1. MySQLの低速クエリログに対して`pt-query-digest --type=slowlog` コマンドを実行します。
   * 低速なクエリログの場所を確認するには、開発者ドキュメントの&#x200B;**[[!UICONTROL Log locations > Service Logs]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)**&#x200B;を参照してください。
   * [[!DNL Percona Toolkit] > pt-query-digest](https://www.percona.com/doc/percona-toolkit/LATEST/pt-query-digest.html#pt-query-digest) ドキュメントを参照してください。
1. 見つかった問題に基づいて、クエリを修正する手順を実行し、より迅速に実行します。

## MySQLの「プロセスリスト」の確認

### 説明

これは、MySQL サーバーが有効かどうか、およびスタックしたクエリがないかどうかを特定するのに役立ちます。

### 手順

1. MySQL コマンドライン（Adobe Commerce オンプレミス/Magento Open Source）またはコマンドライン（Adobe Commerce オンクラウドインフラストラクチャ）からクラウドサーバーにログインします。
1. 以下のコードブロックを使用してMySQLにログインします。 これにより、ログインのプロセスが自動化されます。

   ```MySQL
   `export DB_NAME=$(grep [\']db[\'] -A 20 app/etc/env.php | grep dbname | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/['][,]//");    export MYSQL_HOST=$(grep [\']db[\'] -A 20 app/etc/env.php | grep host | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/['][,]//");    export DB_USER=$(grep [\']db[\'] -A 20 app/etc/env.php | grep username | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/['][,]//");    export MYSQL_PWD=$(grep [\']db[\'] -A 20 app/etc/env.php | grep password | head -n1 | sed "s/.*[=][>][ ]*[']//" | sed "s/[']$//" | sed "s/['][,]//");    mysql -h $MYSQL_HOST -u $DB_USER --password=$MYSQL_PWD $DB_NAME -U -A -e 'show processlist;`
   ```

1. エラーが発生した場合、または応答に30秒以上かかる場合は、サポートに連絡してMySQL サーバーを確認する必要があります。
1. サンプル出力の確認。

1. 出力の例を次に示します。

   ```MySQL
   `$ mysql -h $MYSQL_HOST -u $DB_USER --password=$MYSQL_PWD $DB_NAME -U -A -e 'show processlist;'    +-----------+---------------+--------------------+---------------+---------+------+----------------+------------------------------------------------------------------------------------------------------+----------+    | Id        | User          | Host               | db            | Command | Time | State          | Info                                                                                                 | Progress |    +-----------+---------------+--------------------+---------------+---------+------+----------------+------------------------------------------------------------------------------------------------------+----------+    | 123456789 | abcdefghijklm | 192.168.7.10:12345 | abcdefghijklm | Query   |    0 | Writing to net | SELECT `magento_versionscms_hierarchy_node`.*, `page_table`.`title` AS `page_title`, `page_table`.`i |    0.000 |    | 123456788 | abcdefghijklm | 192.168.7.10:12344 | abcdefghijklm | Sleep   |    0 |                | NULL                                                                                                 |    0.000 |    | 123456777 | abcdefghijklm | 192.168.7.10:12333 | abcdefghijklm | Sleep   |    0 |                | NULL                                                                                                 |    0.000 |    | 123456666 | abcdefghijklm | 192.168.5.8:12222  | abcdefghijklm | Sleep   |    0 |                | NULL                                                                                                 |    0.000 |`
   ```

1. 「時間」列を1800秒を超える時間にチェックします。これは、プロセスの完了に時間がかかりすぎている可能性があることを示します。 「状態」列のプロセスのステータスをメモします。
1. クエリを確認し、その期間の実行が期待されない場合は、クエリを強制終了する可能性があります。 長時間実行中のクエリが予想される可能性があります。


## 関連トピックス

* dev.mysql.comの[MySQL Show Processlist Syntax](https://dev.mysql.com/doc/refman/8.0/en/show-processlist.html)。
* dev.mysql.comの[MySQL Kill Syntax](https://dev.mysql.com/doc/refman/8.0/en/kill.html)。
* 開発者ドキュメントの[ セキュリティ、パフォーマンス、データ処理](https://developer.adobe.com/commerce/php/best-practices/extensions/security/)。
* 開発者向けドキュメントの[MySQL ヘルプ ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql)。
