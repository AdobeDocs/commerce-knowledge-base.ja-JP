---
title: クラウド上のAdobe CommerceでMySQL Serverが消えました​エラー
description: この記事では、「cron.log」ファイルに「*SQL サーバーが消えた*」エラーメッセージが表示される問題の解決策について説明します。 画像ファイルの読み込みの問題やデプロイメントの失敗など、さまざまな問題が発生する可能性があります。
exl-id: 14cb9a6d-6d25-4044-8f52-d65648c03431
feature: Cloud, Paas, Services, Variables
role: Developer
source-git-commit: be0c72a1759ba172666c7c9409c65a1a388e3f11
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# クラウド上のAdobe CommerceでMySQL Serverが消えました&#x200B;エラー

この記事では、`cron.log` ファイルで「*SQL サーバーが消えました*」というエラーメッセージが表示される問題の解決策について説明します。 画像ファイルの読み込みの問題やデプロイメントの失敗など、さまざまな問題が発生する可能性があります。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、すべての[ サポートされているバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## イシュー

`cron.log` ファイルに「*SQL サーバーが消えました*」というエラーメッセージが表示されます。

<u>複製する手順</u>

ファイルを読み込み、デプロイメントをトリガーします。

<u>期待される結果</u>

デプロイメントの成功：

<u>実際の結果</u>

`cron.log`のエラーメッセージ :&quot; *SQLSTATE\[HY000\] \[2006\] MySQL サーバーが消えましたat/app/AAAAAAAAA/vendor/magento/zendframework1/library/Zend/Db/Adapter/Pdo/Abstract.php:144&quot;*

## 原因

`default_socket_timeout`の値が低すぎます。 これは、設定`default_socket_timeout`が原因です。 phpがこの期間内にMySQL データベースから何も受け取らない場合、phpは接続が切断されていると仮定し、エラーをスローします。

## Solution

1. CLIで実行して、`default_socket_timeout`の現在のタイムアウト期間を確認してください：`php -i |grep default_socket_timeout`
1. タイムアウト設定の増加に応じて、`default_socket_timeout`変数を`/etc/platform/<project_name>/php.ini` ファイルの予想される最長時間に設定します。 10～15分以内に設定することをお勧めします。
1. GITにコミットして再デプロイします。

## 関連トピックス

* [Adobe Commerce on cloud infrastructureのデータベースのベストプラクティス](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html)
* [Adobe Commerceのクラウドインフラストラクチャで最も一般的なデータベースの問題](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html)

