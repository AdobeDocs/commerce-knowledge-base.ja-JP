---
title: クラウドインフラストラクチャ上のAdobe Commerceでのデータベースダンプの作成
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerceにデータベース（DB）ダンプを作成する可能性のある（および推奨される）方法について説明します。
exl-id: 4a2e54ac-8d65-4e51-8337-08f9748dc6c0
feature: Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%
---
# クラウドインフラストラクチャ上のAdobe Commerceでのデータベースダンプの作成

この記事では、クラウドインフラストラクチャ上のAdobe Commerceにデータベース（DB）ダンプを作成する可能性のある（および推奨される）方法について説明します。

DBをダンプするために1つのバリアント（オプション）を使用するだけで済みます。 これらのオプションは、あらゆる種類の環境（統合、ステージング、実稼動）およびプラン（Adobe Commerce on cloud infrastructure Starter プランアーキテクチャおよびAdobe Commerce on cloud infrastructure Pro プランアーキテクチャ）に適用されます。

## 前提条件：環境へのSSH

この記事で説明したバリエーションをAdobe Commerce上のクラウドインフラストラクチャにDBをダンプするには、まず[SSHで環境に接続する必要があります](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。

>[!WARNING]
>
>オプション 1またはオプション 2のどちらを選択しても、データベースセカンダリノードに対してピーク時にコマンドを実行してください。

## オプション 1: db-dump （**ece-tools；推奨**）

[ECE-Tools](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) コマンドを使用してDBをダンプできます。

```php
vendor/bin/ece-tools db-dump
```

これは推奨され、最も安全なオプションです。

Commerce on Cloud Infrastructure ガイドの「[Dump your database （ECE-Tools） ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/database-dump.html)」を参照してください。

## オプション 2: mariadb-dump （または古いバージョンのmysqldump）

+++<b>新しいMariaDB バージョン（11.x以降）の場合</b>

MariaDB 11.0.1以降、`mysqldump` シンボリックリンクは非推奨（廃止予定）です。 代わりに`mariadb-dump`を使用することをお勧めします。

詳しくは、[mariadb-dump クライアントユーティリティ ](https://mariadb.com/docs/server/clients-and-utilities/backup-restore-and-import-clients/mariadb-dump)を参照してください。

+++

+++<b>古いMariaDB バージョンの場合</b> 

`mariadb-dump`が使用できない古いMariaDB バージョンを使用している場合は、ネイティブ MySQL `mysqldump` コマンドを使用してDBをダンプできます。

>[!WARNING]
>
>このコマンドをデータベース・クラスタに対して実行しないでください。 クラスターは、データベースのプライマリに対して実行されるか、セカンダリに対して実行されるかを区別しません。 クラスターがプライマリに対してこのコマンドを実行する場合、データベースはダンプが完了するまで書き込みを実行できず、パフォーマンスとサイトの安定性に影響を与える可能性があります。

コマンド全体は次のようになります。

```sql
mysqldump -h <host> -u <username> -p <password> --single-transaction <db_name> | gzip > /tmp/<dump_name>.sql.gz
```

`mysqldump` コマンドを実行して作成し、`\tmp`に保存したデータベース バックアップは、この場所から移動する必要があります。 `\tmp`のストレージ容量を使用しないでください（問題が発生する可能性があります）。

+++

DB資格情報（ホスト、ユーザー名、パスワード）を取得するには、`MAGENTO_CLOUD_RELATIONSHIPS`環境変数を呼び出します。

```
echo $MAGENTO_CLOUD_RELATIONSHIPS |base64 --d |json_pp
```

**関連ドキュメント：**

* [mysqldump - MySQLの公式ドキュメントのデータベース バックアップ プログラム ](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html)。
* Commerce on Cloud Infrastructure ガイドの[ クラウド固有の変数](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-cloud.html) （`MAGENTO_CLOUD_RELATIONSHIPS`を参照）。
