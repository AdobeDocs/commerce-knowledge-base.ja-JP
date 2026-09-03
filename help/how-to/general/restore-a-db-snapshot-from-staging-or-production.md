---
title: ステージングまたは実稼動環境からのDB スナップショットの復元
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerce上のステージングまたは実稼動環境からDB スナップショットを復元する方法について説明します。
exl-id: 1026a1c9-0ca0-4823-8c07-ec4ff532606a
source-git-commit: 62815213ce54f72d27812b9c2d7b3997f2e88897
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# DB スナップショットを[!DNL Staging]または[!DNL Production]から復元します

この記事では、Cloud Pro インフラストラクチャ上のAdobe Commerceで[!DNL Staging]または[!DNL Production]からDB [!DNL snapshot]を復元する方法について説明します。


>[!NOTE]
>
>これらの方法により、**完全なスナップショット**が復元されます。
>スナップショット **部分**&#x200B;を復元する必要がある場合（例：注文テーブルを完全に残したままカタログテーブルのみを復元する場合など）は、開発者またはDBAに相談する必要があります。


## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、[ サポートされているすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

ケースに最適なものを選択します。

>[!NOTE]
>
> 統合環境にスナップショットを読み込む場合は、データベースのサイズに注意してください。 大規模なデータベースは、インポート後にパフォーマンスの低下を引き起こす可能性があります。 スナップショットをステージング環境またはローカル環境に読み込んでレビューし、サイズを縮小してから統合に転送することをお勧めします。 さらに、インポート後にパフォーマンスの問題が発生した場合は、統合ブランチでcron ジョブを無効にすることを検討してください。 詳しくは、Commerce on Cloud Infrastructure ガイドの[Integration environment](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/pro-architecture#integration-environment)を参照してください。

* [方法1: データベース  [!DNL dump] をローカルマシンに転送し、読み込む](#meth2)。
* [方法2: データベース  [!DNL dump] をサーバー](#meth3)から直接インポートします。

## 方法1: データベース [!DNL dump]をローカル コンピューターに転送してインポートする {#meth2}


>[!NOTE]
>
> **Azure プロジェクト**&#x200B;のスナップショットの形式が異なり、**インポートできない他のデータベースが含まれています**。\
> スナップショットをインポートする前に、ダンプのインポートを続行する前に、適切なデータベースを&#x200B;**抽出**&#x200B;するためにさらなる手順を実行する必要があります。

手順は次のとおりです。

1. [!DNL SFTP]を使用して、データベース [!DNL snapshot]が配置された場所（通常は[!DNL cluster]の最初のサーバー/ノード）に移動します（例：`/mnt/recovery-<recovery_id>`）。
   > **Azure ベースのプロジェクト：**\
   > プロジェクトがAzure ベースの場合（つまり、プロジェクト URLが`https://us-a1.magento.cloud/projects/<cluster_id>`のように見える場合）、スナップショットは次の場所に配置されます。
   > * `/mnt/shared/<cluster ID>/all-databases.sql.gz`
   > * `/mnt/shared/<cluster ID_stg>/all-databases.sql.gz`

   **Azure固有の抽出ステップ**

   実稼動用の&#x200B;**:**

   ```bash
   cd /mnt/shared/<cluster ID>/
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

   **ステージング用：**

   ```bash
   cd /mnt/shared/<cluster ID_stg>/
   gunzip all-databases.sql.gz 
   head -n 17 all-databases.sql > <cluster ID_stg>.sql
   sed -n '/^-- Current Database: `<cluster ID_stg>`/,/^-- Current Database: `/p' all-databases.sql >> <cluster ID_stg>.sql 
   gzip <cluster ID_stg>.sql  
   zcat <cluster ID_stg>.sql.gz | \
   sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | \
   mysql -h 127.0.0.1 \
   -u $DB_USER \
   --password=$MYSQL_PWD $DB_NAME \
   --init-command="SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT ;SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS ;SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION ;SET NAMES utf8 ;SET @OLD_TIME_ZONE=@@TIME_ZONE ;SET TIME_ZONE='+00:00' ;SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 ;SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 ;SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' ;SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0;"
   ```

1. データベース [!DNL dump file] （例：[!DNL Production]には`<cluster ID>.sql.gz`、[!DNL Staging]には`<cluster ID_stg>.sql.gz`）をローカル コンピューターにコピーします。
1. リモートでデータベースに接続するように[!DNL SSH tunnel]を設定していることを確認してください：[[!DNL SSH] および [!DNL sFTP]: [!DNL SSH tunneling]](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#env-start-tunn)。詳しくは、開発者ドキュメントを参照してください。
1. データベースに接続します。

   ```bash
   mysql -h <db-host> -P <db-port> -p -u <db-user> <db-name>
   ```

1. データベース [!DNL Drop]。[!DNL MariaDB] プロンプトで、次のように入力します。

   （[!DNL Production]の場合）

   ```bash
   drop database <cluster ID>;
   ```

   （[!DNL Staging]の場合）

   ```bash
   drop database <cluster ID_stg>;
   ```

1. 次のコマンドを入力して、[!DNL snapshot]を読み込みます。

   （[!DNL Production]の場合）

   ```bash
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

   （[!DNL Staging]の場合）

   ```bash
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

## 方法2: データベース [!DNL dump]をサーバーから直接インポートする {#meth3}

手順は次のとおりです。

1. データベース [!DNL snapshot]が配置された場所（通常は[!DNL cluster]の最初のサーバー/ノード）に移動します（例：`/mnt/recovery-<recovery_id>`）。
1. [!DNL drop]にクラウドデータベースを再作成するには、まずデータベースに接続します。

   ```bash
   mysql -h 127.0.0.1 -P <db-port> -p -u <db-user> <db-name>
   ```

1. データベース [!DNL Drop]。[!DNL MariaDB] プロンプトで、次のように入力します。

   （[!DNL Production]の場合）

   ```bash
   drop database <cluster ID>;
   ```

   （[!DNL Staging]の場合）

   ```bash
   drop database <cluster ID_stg>;
   ```

1. データベースを削除した後、データベースを再作成します。

   ```bash
   create database [database_name];
   ```

1. 次のコマンドを入力して、[!DNL snapshot]を読み込みます。

   （データベースのバックアップを[!DNL Production]からインポートする場合）

   ```bash
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （データベースのバックアップを[!DNL Staging]からインポートする場合）

   ```bash
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップをインポートする場合）

   ```bash
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップをインポートする場合）

   ```bash
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

## 関連トピックス

アドビの開発者ドキュメントには、次のようなものがあります。

* [コードの読み込み：データベースの読み込み](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production)
* [[!DNL Snapshots]および [!DNL backup] 管理： [!DNL Dump] あなたのデータベース](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)
* [クラウドでのバックアップ（スナップショット）:FAQ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/faq/backup-snapshot-on-cloud-faq)
