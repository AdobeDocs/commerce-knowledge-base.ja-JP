---
title: クラウドインフラストラクチャ上のAdobe Commerceにデータベースダンプを作成する
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerceにデータベース（DB）ダンプを作成する方法として考えられる（推奨される）方法について説明します。
exl-id: 4a2e54ac-8d65-4e51-8337-08f9748dc6c0
feature: Cloud
source-git-commit: 0948b2a94ee4f2a355e7c024a09929f0ad223783
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# クラウドインフラストラクチャ上のAdobe Commerceにデータベースダンプを作成する

この記事では、クラウドインフラストラクチャ上のAdobe Commerceにデータベース（DB）ダンプを作成する方法として考えられる（推奨される）方法について説明します。

データベースのダンプに必要なのは、1 つのバリアント （オプション）だけです。 これらのオプションは、任意の環境タイプ（統合、ステージング、実稼動）および任意のプラン（クラウドインフラストラクチャー上のAdobe Commerce スタータープランアーキテクチャおよびクラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ）に適用されます。

## 前提条件：環境に SSH で接続する

この記事で説明したバリアントを使用してクラウドインフラストラクチャ上のAdobe Commerceに DB をダンプするには、最初に以下を行う必要があります [環境に SSH で接続する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html).

>[!WARNING]
>
>オプション 1 とオプション 2 のどちらを選択する場合でも、データベースのセカンダリノードに対してピーク時を避けてコマンドを実行してください。

## オプション 1:db-dump （**ece-tools；推奨**）

を使用して DB をダンプできます。 [ECE-Tools](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package.html) コマンド：

```php
vendor/bin/ece-tools db-dump
```

これは推奨される最も安全なオプションです。

参照： [データベースのダンプ（ECE-Tools）](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/database-dump.html) クラウドインフラストラクチャーに関するCommerceのガイドを参照してください。

## オプション 2:mysqldump

>[!WARNING]
>
>データベースクラスタに対してこのコマンドを実行しないでください。 クラスターは、データベースのプライマリに対して実行されるか、セカンダリに対して実行されるかを区別しません。 クラスターがプライマリに対してこのコマンドを実行すると、ダンプが完了するまでデータベースは書き込みを実行できず、パフォーマンスとサイトの安定性に影響を与える可能性があります。

ネイティブの MySQL を使用して DB をダンプできます。 `mysqldump` コマンド。

コマンド全体は次のようになります。

```sql
mysqldump -h <host> -u <username> -p <password> --single-transaction <db_name> | gzip > /tmp/<dump_name>.sql.gz
```

を実行して作成されたデータベースのバックアップ `mysqldump` コマンドと保存済みファイル `\tmp`、をこの場所から移動する必要があります。 のストレージスペースを消費しないようにします `\tmp` （問題が発生する可能性があります）。

DB の資格情報（ホスト、ユーザー名、パスワード）を取得するには、 `MAGENTO_CLOUD_RELATIONSHIPS` 環境変数：

```
echo $MAGENTO_CLOUD_RELATIONSHIPS |base64 --d |json_pp
```

**関連ドキュメント：**

* [mysqldump - データベースバックアッププログラム](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) の公式 MySQL ドキュメントを参照してください。
* [クラウド固有の変数](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-cloud.html) （を参照） `MAGENTO_CLOUD_RELATIONSHIPS`）を参照してください。Commerce on Cloud Infrastructure ガイドをご覧ください。
