---
title: クラウドインフラストラクチャ上のAdobe Commerceにデータベースダンプを作成する
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerceにデータベース（DB）ダンプを作成する方法として考えられる（推奨される）方法について説明します。
exl-id: 4a2e54ac-8d65-4e51-8337-08f9748dc6c0
feature: Cloud
source-git-commit: 96b145a1f76c296907da96fd97c7a8f7778463f8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# クラウドインフラストラクチャ上のAdobe Commerceにデータベースダンプを作成する

この記事では、クラウドインフラストラクチャ上のAdobe Commerceにデータベース（DB）ダンプを作成する方法として考えられる（推奨される）方法について説明します。

データベースのダンプに必要なのは、1 つのバリアント （オプション）だけです。 これらのオプションは、任意の環境タイプ（統合、ステージング、実稼動）および任意のプラン（クラウドインフラストラクチャー上のAdobe Commerce スタータープランアーキテクチャおよびクラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ）に適用されます。

## 前提条件：環境に SSH で接続する

この記事で説明されているバリアントを使用してクラウドインフラストラクチャ上のAdobe Commerceに DB をダンプするには、まず [ 環境に SSH 接続 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) する必要があります。

>[!WARNING]
>
>オプション 1 とオプション 2 のどちらを選択する場合でも、データベースのセカンダリノードに対してピーク時を避けてコマンドを実行してください。

## オプション 1:db-dump （**ece-tools；推奨**）

[ECE-Tools](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) コマンドを使用して DB をダンプできます。

```php
vendor/bin/ece-tools db-dump
```

これは推奨される最も安全なオプションです。

クラウドインフラストラクチャー上のCommerce ガイドの [ データベースのダンプ（ECE-Tools） ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/database-dump.html) を参照してください。

## オプション 2:mariadb-dump （古いバージョンでは mysqldump）

+++<b> 新しい MariaDB バージョン（11.x 以降） </b>

MariaDB 11.0.1 以降、`mysqldump` シンボリックリンクは非推奨になりました。 代わりに、`mariadb-dump` を使用することをお勧めします。

詳しくは、[mariadb-dump クライアントユーティリティ ](https://mariadb.com/docs/server/clients-and-utilities/backup-restore-and-import-clients/mariadb-dump) を参照してください。

+++

+++<b> 古いバージョンの MariaDB の場合 </b> 

`mariadb-dump` が利用できない古い MariaDB バージョンを使用している場合は、ネイティブの MySQL `mysqldump` コマンドを使用して DB をダンプできます。

>[!WARNING]
>
>データベースクラスタに対してこのコマンドを実行しないでください。 クラスターは、データベースのプライマリに対して実行されるか、セカンダリに対して実行されるかを区別しません。 クラスターがプライマリに対してこのコマンドを実行すると、ダンプが完了するまでデータベースは書き込みを実行できず、パフォーマンスとサイトの安定性に影響を与える可能性があります。

コマンド全体は次のようになります。

```sql
mysqldump -h <host> -u <username> -p <password> --single-transaction <db_name> | gzip > /tmp/<dump_name>.sql.gz
```

`mysqldump` コマンドを実行して作成し、`\tmp` に保存したデータベースのバックアップは、この場所から移動する必要があります。 `\tmp` のストレージスペースを消費しないでください（問題が発生する可能性があります）。

+++

DB 資格情報（ホスト、ユーザー名およびパスワード）を取得するには、`MAGENTO_CLOUD_RELATIONSHIPS` の環境変数を呼び出します。

```
echo $MAGENTO_CLOUD_RELATIONSHIPS |base64 --d |json_pp
```

**関連ドキュメント：**

* [mysqldump - データベースバックアッププログラム ](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) 公式の MySQL ドキュメントにあります。
* [ クラウド固有の変数 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-cloud.html) （`MAGENTO_CLOUD_RELATIONSHIPS` を参照） – Commerce on Cloud Infrastructure ガイドを参照してください。
