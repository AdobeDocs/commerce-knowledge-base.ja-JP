---
title: ステージング環境または実稼動環境から DB スナップショットを復元
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceでステージング環境または実稼動環境から DB スナップショットを復元する方法について説明します。
exl-id: 1026a1c9-0ca0-4823-8c07-ec4ff532606a
source-git-commit: ad0ec2e6dc1d3e1023ad4ecda595b5c942716407
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# から DB スナップショットをリストアする [!DNL Staging] または [!DNL Production]

この記事では、DB の復元方法を説明します [!DNL snapshot] から [!DNL Staging] または [!DNL Production] （Cloud Pro インフラストラクチャ上のAdobe Commerce上）。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

お客様の状況に最も適したものを選択してください。

* [方法 1：データベースを転送する [!DNL dump] ローカルマシンに追加して読み込みます。](#meth2).
* [方法 2：データベースをインポートする [!DNL dump] サーバーから直接](#meth3).

## 方法 1：データベースを転送する [!DNL dump] ローカルマシンに追加して読み込みます。 {#meth2}

手順は次のとおりです。

1. 使用 [!DNL sFTP]で、データベースがある場所に移動します。 [!DNL snapshot] が（通常はユーザーの最初のサーバーやノードに）配置されている [!DNL cluster] （例： `/mnt/recovery-<recovery_id>`）に設定します。 メモ：プロジェクトが Azure ベースの場合、プロジェクト URL はhttps://us-a1.magento.cloud/projects/のようになります。&lt;cluster_id>を選択すると、スナップショットはに配置されます。 `/mnt/shared/<cluster ID>/all-databases.sql.gz` または `/mnt/shared/<cluster ID_stg>/all-databases.sql.gz` その代わり。

   メモ : Azure プロジェクトのスナップショットの形式は異なり、インポートできない他のデータベースが含まれます。 スナップショットをインポートする前に、ダンプをインポートする前に、適切なデータベースを抽出するための追加手順を実行する必要があります。

   実稼動の場合：

   ```sql
   cd /mnt/shared/<cluster ID/
   gunzip all-databases.sql.gz 
   head -n 17 all-databases.sql > <cluster ID>.sql 
   sed -n '/^-- Current Database: `<cluster ID>`/,/^-- Current Database: `/p' all-databases.sql >> <cluster ID>.sql gzip <cluster ID>.sql
   zcat <cluster ID>.sql.gz | \
   sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | \
   mysql -h 127.0.0.1 \
   -u $DB_USER \
   --password=$MYSQL_PWD $DB_NAME \
   --init-command="SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT ;SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS ;SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION ;SET NAMES utf8 ;SET @OLD_TIME_ZONE=@@TIME_ZONE ;SET TIME_ZONE='+00:00' ;SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 ;SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 ;SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' ;SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0;"
   ```

   ステージング用：

   ```sql
   cd /mnt/shared/<cluster ID/ | cd /mnt/shared/<cluster ID_stg>
   gunzip all-databases.sql.gz 
   head -n 17 all-databases.sql > <cluster ID_stg>.sql
   sed -n '/^-- Current Database: `wyf2o4zlrljjs`/,/^-- Current Database: `/p' all-databases.sql >> <cluster ID_stg>.sql 
   gzip <cluster ID_stg>.sql  
   zcat <cluster ID_stg>.sql.gz | \
   sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | \
   mysql -h 127.0.0.1 \
   -u $DB_USER \
   --password=$MYSQL_PWD $DB_NAME \
   --init-command="SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT ;SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS ;SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION ;SET NAMES utf8 ;SET @OLD_TIME_ZONE=@@TIME_ZONE ;SET TIME_ZONE='+00:00' ;SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 ;SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 ;SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' ;SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0;"
   ```

1. データベースをコピーします [!DNL dump file] （例： `<cluster ID>.sql.gz` （用） [!DNL Production] または `<cluster ID_stg>.sql.gz` （用） [!DNL Staging]）をローカルコンピューターに追加します。
1. を設定したことを確認します [!DNL SSH tunnel] データベースにリモートで接続するには： [[!DNL SSH] および [!DNL sFTP]: [!DNL SSH tunneling]](https://devdocs.magento.com/cloud/env/environments-ssh.html#env-start-tunn) 開発者向けドキュメントを参照してください。
1. データベースに接続します。

   ```sql
   mysql -h <db-host> -P <db-port> -p -u <db-user> <db-name>
   ```

1. [!DNL Drop] データベース（） [!DNL MariaDB] プロンプトで、次のように入力します。

   （用 [!DNL Production]）

   ```sql
   drop database <cluster ID>;
   ```

   （用 [!DNL Staging]）

   ```sql
   drop database <cluster ID_stg>;
   ```

1. 次のコマンドを入力して、 [!DNL snapshot]:

   （用 [!DNL Production]）

   ```sql
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

   （用 [!DNL Staging]）

   ```sql
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

## 方法 2：データベースをインポートする [!DNL dump] サーバーから直接 {#meth3}

手順は次のとおりです。

1. データベースがある場所に移動します。 [!DNL snapshot] が（通常はユーザーの最初のサーバーやノードに）配置されている [!DNL cluster] （例： `/mnt/recovery-<recovery_id>`）に設定します。
1. 終了 [!DNL drop] クラウドデータベースを再作成するには、まずデータベースに接続します。

   ```sql
   mysql -h 127.0.0.1 -P <db-port> -p -u <db-user> <db-name>
   ```

1. [!DNL Drop] データベース（） [!DNL MariaDB] プロンプトで、次のように入力します。

   （用 [!DNL Production]）

   ```sql
   drop database <cluster ID>;
   ```

   （用 [!DNL Staging]）

   ```sql
   drop database <cluster ID_stg>;
   ```

1. 次のコマンドを入力して、 [!DNL snapshot]:

   （データベース バックアップのインポート元： [!DNL Production]）

   ```sql
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （データベース バックアップのインポート元： [!DNL Staging]）

   ```sql
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップを読み込む場合）

   ```sql
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

## 関連資料

開発者向けドキュメントでは、

* [コードのインポート：データベースをインポートします](https://devdocs.magento.com/cloud/setup/first-time-setup-import-import.html#cloud-import-db)
* [[!DNL Snapshots] および [!DNL backup] 管理： [!DNL Dump] データベース](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump)
