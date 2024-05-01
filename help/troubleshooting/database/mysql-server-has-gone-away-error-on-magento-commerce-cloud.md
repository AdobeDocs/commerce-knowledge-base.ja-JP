---
title: MySQL サーバーが廃止されました​ クラウド上のAdobe Commerceのエラー
description: この記事では、「cron.log」ファイルに「*SQL server has gone away*」というエラーメッセージが表示される問題の解決策について説明します。 画像ファイルの読み込みの問題やデプロイメントの失敗など、様々な症状が発生することがあります。
exl-id: 14cb9a6d-6d25-4044-8f52-d65648c03431
feature: Cloud, Paas, Services, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# MySQL サーバーが廃止されました&#x200B; クラウド上のAdobe Commerceのエラー

この記事では、が届いた問題の解決策について説明します。」 *SQL Server が使用できなくなりました* のエラーメッセージ `cron.log` ファイル。 画像ファイルの読み込みの問題やデプロイメントの失敗など、様々な症状が発生することがあります。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf).

## 問題

「」が届きます *SQL Server が使用できなくなりました* のエラーメッセージ `cron.log` ファイル。

<u>再現手順</u>

ファイルを読み込んで、のデプロイメントをトリガーします。

<u>期待される結果</u>

正常なデプロイメント。

<u>実際の結果</u>

のエラーメッセージ `cron.log` :&quot; *SQLSTATE\[HY000\] \[2006\] MySQL Server has gone away at/app/AAAAAAAAA/vendor/magento/zendframework1/library/Zend/Db/Adapter/Pdo/Abstract.php:144&quot;*

## 原因：

この `default_socket_timeout` 値の設定値が低すぎる。 これは、の設定が原因です `default_socket_timeout` . この期間内に php が MySQL データベースから何も受け取らない場合、php は接続解除されていると見なし、エラーをスローします。

## 解決策

1. の現在のタイムアウト期間を確認します `default_socket_timeout` CLI でを実行することにより、次の操作を行います。    ```    php -i |grep default_socket_timeout    ```
1. タイムアウト設定の増加に応じて、は `default_socket_timeout` 内で予想される最長実行時間に対する変数 `/etc/platform/<project_name>/php.ini` ファイル。 10～15 分の間に設定することをお勧めします。
1. GIT にコミットし、再デプロイします。

## 関連資料

* [データベースのアップロードにより MySQL への接続が失われる](/help/troubleshooting/database/database-upload-loses-connection-to-mysql.md)
* [クラウドインフラストラクチャー上のAdobe Commerceに関するデータベースのベストプラクティス](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html)
* [クラウドインフラストラクチャー上のAdobe Commerceで最も一般的なデータベースの問題](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html)
