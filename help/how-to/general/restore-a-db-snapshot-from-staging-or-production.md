---
title: ステージング環境または実稼動環境から DB スナップショットを復元
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceでステージング環境または実稼動環境から DB スナップショットを復元する方法について説明します。
exl-id: 1026a1c9-0ca0-4823-8c07-ec4ff532606a
source-git-commit: 62815213ce54f72d27812b9c2d7b3997f2e88897
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# [!DNL Staging] または [!DNL Production] から DB スナップショットをリストアする

この記事では、Cloud Pro インフラストラクチャ上のAdobe Commerceで [!DNL snapshot] または [!DNL Staging] から DB [!DNL Production] を復元する方法について説明します。


>[!NOTE]
>
>これらの方法では、**完全なスナップショット** が復元されます。
>&#x200B;>スナップショットを **部分的に** リストアする必要がある場合（たとえば、順序テーブルはそのままにしてカタログテーブルだけをリストアする場合）、開発者または DBA に相談する必要があります。


## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[&#x200B; サポート対象のすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

お客様の状況に最も適したものを選択してください。

>[!NOTE]
>
> スナップショットを統合環境にインポートする場合は、データベースのサイズに注意してください。 データベースが大きいと、インポート後にパフォーマンスが低下する場合があります。 最初にスナップショットをステージング環境またはローカル環境にインポートして、確認しサイズを小さくしてから統合に転送することをお勧めします。 さらに、インポート後にパフォーマンスの問題が発生した場合は、統合ブランチで cron ジョブを無効にすることを検討します。 詳しくは、『クラウドインフラストラクチャー上のCommerce』ガイドの [&#x200B; 統合環境 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/pro-architecture#integration-environment) を参照してください。

* [&#x200B; 方法 1：データベースをローカルマシンに転送し  [!DNL dump]  読み込みます &#x200B;](#meth2)。
* [&#x200B; 方法 2：サーバーからデータベース  [!DNL dump]  直接インポート &#x200B;](#meth3)。

## 方法 1: データベース [!DNL dump] をローカル マシンに転送し、インポートする {#meth2}


>[!NOTE]
>
> **Azure プロジェクト** のスナップショットの形式は異なり、他のデータベース **インポートできません** が含まれています。\
> スナップショットを読み込む前に、ダンプの読み込みを続行する前に、追加の手順を実行して **適切なデータベースを抽出** する必要があります。

手順は次のとおりです。

1. [!DNL SFTP] を使用して、データベース [!DNL snapshot] が配置されている場所（通常は [!DNL cluster] の最初のサーバー/ノード）に移動します（例：`/mnt/recovery-<recovery_id>`）。
   > **Azure ベースのプロジェクト：**\
   > プロジェクトが Azure ベースの場合（つまり、プロジェクト URL が `https://us-a1.magento.cloud/projects/<cluster_id>` のような場合）、スナップショットは次の場所に配置されます。
   > * `/mnt/shared/<cluster ID>/all-databases.sql.gz`
   > * `/mnt/shared/<cluster ID_stg>/all-databases.sql.gz`

   **Azure 固有の抽出手順**

   **実稼動の場合：**

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

1. データベース [!DNL dump file] （例：`<cluster ID>.sql.gz` の場合は [!DNL Production]、`<cluster ID_stg>.sql.gz` の場合は [!DNL Staging]）をローカルコンピューターにコピーします。
1. 開発者向けドキュメントで、データベースにリモートで接続する [!DNL SSH tunnel] を [[!DNL SSH]  および  [!DNL sFTP]: [!DNL SSH tunneling]](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#env-start-tunn) のように設定していることを確認します。
1. データベースに接続します。

   ```bash
   mysql -h <db-host> -P <db-port> -p -u <db-user> <db-name>
   ```

1. データベース [!DNL Drop]、[!DNL MariaDB] のプロンプトに対して、次のように入力します。

   （[!DNL Production] 用）

   ```bash
   drop database <cluster ID>;
   ```

   （[!DNL Staging] 用）

   ```bash
   drop database <cluster ID_stg>;
   ```

1. 次のコマンドを入力して [!DNL snapshot] を読み込みます。

   （[!DNL Production] 用）

   ```bash
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

   （[!DNL Staging] 用）

   ```bash
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -P <db-port> -p -u   <db-user> <db-name>
   ```

## 方法 2：サーバーからデータベース [!DNL dump] を直接インポートする {#meth3}

手順は次のとおりです。

1. データベース [!DNL snapshot] が配置されている場所に移動します。通常は [!DNL cluster] の最初のサーバー/ノードに移動します（例：`/mnt/recovery-<recovery_id>`）。
1. クラウドデータベースを [!DNL drop] 成して再作成するには、まずデータベースに接続します。

   ```bash
   mysql -h 127.0.0.1 -P <db-port> -p -u <db-user> <db-name>
   ```

1. データベース [!DNL Drop]、[!DNL MariaDB] のプロンプトに対して、次のように入力します。

   （[!DNL Production] 用）

   ```bash
   drop database <cluster ID>;
   ```

   （[!DNL Staging] 用）

   ```bash
   drop database <cluster ID_stg>;
   ```

1. データベースを削除した後、データベースを再作成します。

   ```bash
   create database [database_name];
   ```

1. 次のコマンドを入力して [!DNL snapshot] を読み込みます。

   （[!DNL Production] からデータベース バックアップをインポートする場合）

   ```bash
   zcat <cluster ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （[!DNL Staging] からデータベース バックアップをインポートする場合）

   ```bash
   zcat <cluster ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップを読み込む場合）

   ```bash
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

   （他の環境からデータベースバックアップを読み込む場合）

   ```bash
   zcat <database-backup-name>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <db-user> <db-name>
   ```

## 関連資料

開発者向けドキュメントでは、

* [&#x200B; コードのインポート：データベースをインポートします &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production)。
* [[!DNL Snapshots] and [!DNL backup] management: [!DNL Dump]  データベース &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)
* [&#x200B; クラウド上のバックアップ（スナップショット）：よくある質問 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/faq/backup-snapshot-on-cloud-faq)
