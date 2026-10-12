---
title: クラウド上のAdobe CommerceでMySQL Serverが消えました​エラー
description: この記事では、「cron.log」ファイルに「*SQL サーバーが消えた*」エラーメッセージが表示される問題の解決策について説明します。 画像ファイルの読み込みの問題やデプロイメントの失敗など、さまざまな問題が発生する可能性があります。
exl-id: 14cb9a6d-6d25-4044-8f52-d65648c03431
feature: Cloud, Paas, Services, Variables
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
subfeature_v2:
  - id: 2191e157-828a-5358-ad69-ebcaa8402915
    internal-label: Variables
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '312'
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

1. CLI `php -i |grep default_socket_timeout`で実行して、`default_socket_timeout`の現在のタイムアウト期間を確認してください。
1. CLIで実行して、`default_socket_timeout`の現在のタイムアウト期間を確認してください：`php -i |grep default_socket_timeout`
1. タイムアウト設定の増加に応じて、`default_socket_timeout`変数を`/etc/platform/<project_name>/php.ini` ファイルの予想される最長時間に設定します。 10～15分以内に設定することをお勧めします。
1. GITにコミットして再デプロイします。

## 関連トピックス

* [Adobe Commerce on cloud infrastructureのデータベースのベストプラクティス](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html)
* [Adobe Commerceのクラウドインフラストラクチャで最も一般的なデータベースの問題](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html)
