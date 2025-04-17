---
title: ステージング環境または実稼動環境から DB スナップショットを復元
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceでステージング環境または実稼動環境から DB スナップショットを復元する方法について説明します。
exl-id: 1026a1c9-0ca0-4823-8c07-ec4ff532606a
source-git-commit: c8cd2bf97681527a32a403a413c5fa823d07abed
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# [!DNL Staging] または [!DNL Production] から DB スナップショットをリストアする

この記事では、Cloud Pro インフラストラクチャ上のAdobe Commerceで [!DNL Staging] または [!DNL Production] から DB [!DNL snapshot] を復元する方法について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

お客様の状況に最も適したものを選択してください。

* [ 方法 1：データベースをローカルマシンに転送し  [!DNL dump]  読み込みます ](#meth2)。
* [ 方法 2：サーバーからデータベース  [!DNL dump]  直接インポート ](#meth3)。

## 方法 1: データベース [!DNL dump] をローカル マシンに転送し、インポートする {#meth2}

手順は次のとおりです。

1. [!DNL SFTP] を使用して、データベース [!DNL snapshot] が配置されている場所（通常は [!DNL cluster] の最初のサーバー/ノード）に移動します（例：`/mnt/recovery-<recovery_id>`）。 メモ：プロジェクトが Azure ベースの場合（例：プロジェクト URL がhttps://us-a1.magento.cloud/projects/&lt;cluster_id> のような場合）、スナップショットは代わりに `/mnt/shared/<cluster ID>/all-databases.sql.gz` または `/mnt/shared/<cluster ID_stg>/all-databases.sql.gz` に配置されます。

   メモ : Azure プロジェクトのスナップショットの形式は異なり、インポートできない他のデータベースが含まれます。 スナップショットを読み込む前に、次の操作を行います     ダンプをインポートする前に、適切なデータベースを抽出するための追加手順を実行する必要があります。

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

1. データベース [!DNL dump file] （例：[!DNL Production] の場合は `<cluster ID>.sql.gz`、[!DNL Staging] の場合は `<cluster ID_stg>.sql.gz`）をローカルコンピューターにコピーします。
1. 開発者向けドキュメントで、データベースにリモートで接続する [!DNL SSH tunnel] を [[!DNL SSH]  および  [!DNL sFTP]: [!DNL SSH tunneling]](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#env-start-tunn) のように設定していることを確認します。
1. データベースに接続します。

   ```sql
   mysql -h <db-host> -P <db-port> -p -u <db-user> <db-name>
   ```

1. データベース [!DNL Drop]、[!DNL MariaDB] のプロンプトに対して、次のように入力します。

   （[!DNL Production] 用）

   ```sql
   drop database <cluster ID>;
   ```

   （[!DNL Staging] 用）

   ```sql
   drop database <cluster ID_stg>;
   ```

1. 次のコマンドを入力して [!DNL snapshot] を読み込みます。

   （[!DNL Production] 用）

   ```sql
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

   （[!DNL Staging] 用）

   ```sql
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

## 方法 2：サーバーからデータベース [!DNL dump] を直接インポートする {#meth3}

手順は次のとおりです。

1. データベース [!DNL snapshot] が配置されている場所に移動します。通常は [!DNL cluster] の最初のサーバー/ノードに移動します（例：`/mnt/recovery-<recovery_id>`）。
1. クラウドデータベースを [!DNL drop] 成して再作成するには、まずデータベースに接続します。

   ```sql
   mysql -h 127.0.0.1 -P <db-port> -p -u <db-user> <db-name>
   ```

1. データベース [!DNL Drop]、[!DNL MariaDB] のプロンプトに対して、次のように入力します。

   （[!DNL Production] 用）

   ```sql
   drop database <cluster ID>;
   ```

   （[!DNL Staging] 用）

   ```sql
   drop database <cluster ID_stg>;
   ```

1. データベースを削除した後、データベースを再作成します。

   ```mysql
   create database [database_name];
   ```

1. 次のコマンドを入力して [!DNL snapshot] を読み込みます。

   （[!DNL Production] からデータベース バックアップをインポートする場合）

   ```sql
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （[!DNL Staging] からデータベース バックアップをインポートする場合）

   ```sql
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップを読み込む場合）

   ```sql
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップを読み込む場合）

   ```sql
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

## 関連資料

開発者向けドキュメントでは、

* [ コードのインポート：データベースをインポートします ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production)。
* [[!DNL Snapshots] and [!DNL backup] management: [!DNL Dump]  データベース ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)
