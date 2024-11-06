---
title: データベースのアップロードにより MySQL への接続が失われる
description: この記事では、データベースのアップロードによって MySQL への接続が失われた場合の解決策を説明します。
exl-id: 6051cea1-8292-4a81-8908-eb516cb4a32b
feature: Services
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# データベースのアップロードにより MySQL への接続が失われる

この記事では、データベースのアップロードによって MySQL への接続が失われた場合の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.2.x.、2.3.x

## 問題

データベースは、クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ上のプライマリ/統合ブランチや、クラウドインフラストラクチャー上のAdobe Commerce Starter プランアーキテクチャ上のブランチにはアップロードされません。接続できないという症状が発生します。 このエラーは CLI に表示されます。

```
web@ddc35c264bd89a72042f1f3e5a:~$ mysql -h database.internal -u user -p main
Enter password:
ERROR 2013 (HY000): Lost connection to MySQL server at 'reading initial communication packet', system error: 0 "Internal error/check (Not system error)"
```

## 原因：

これは通常、データベースをインポートするためのディスク領域の不足が原因です。

## 解決策

ディスク容量が不足していないかどうかを確認します。 これを行うには、データベース・ポート 3306 に対して CLI で `netcat` コマンドを実行します。このコマンドがフルの場合、ディスク・フル・メッセージが表示されます。

```
web@ddc35c264bd89a72042f1f3e5a:~$ nc database.internal 3306
Database out of space
```

未使用のスペースがある場合は、`services.yaml` ージ内のデータベースに割り当てるスペースを増やし、をデプロイする必要があります。 手順については、「[ サービスディスク容量 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space#service-disk-space)」を参照してください。

注：Pro アーキテクチャ計画では、次のコマンドを実行して、パーティションの割り当て済み領域を確認できます。`df -h`

次のような出力が期待されます。 この例では、割り当てられた 25 GB のうち 10 GB が使用され、15 GB の MySQL 領域は使用されません。

```
f240jestone3wt@i-087r2a25fdac80726:~$ df -h|grep 'File\|xvd'
Filesystem                                         Size  Used Avail Use% Mounted on
/dev/xvda1                                          59G   15G   42G  26% /
/dev/xvdj                                           25G   10G   15G  41% /data/mysql
/dev/xvdi                                           25G   22G  2.6G  90% /data/exports
```

## 関連資料

開発者向けドキュメントの [ ディスク容量の管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space)
