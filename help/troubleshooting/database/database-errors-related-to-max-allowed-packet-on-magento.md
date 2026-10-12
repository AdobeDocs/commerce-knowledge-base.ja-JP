---
title: Adobe Commerceでのmax_allowed_packetに関連するデータベース エラー
description: この記事では、多数の製品をインポートする場合や、デフォルトの16MBよりも大きい「max_allowed_packet」で設定されたパケットよりも大きなパケットをサーバーに処理させる別のタスクを実行する場合に発生する可能性のある、「var/log/exception.log」のデータベース接続エラーの解決策を提供します。
exl-id: e8932b72-91a3-43ea-800e-a6c7a5a17656
feature: Best Practices, Observability, Services
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%
---
# Adobe Commerceでのmax_allowed_packetに関連するデータベース エラー

この記事では、多数の製品をインポートする場合や、サーバーがデフォルトの16 MBよりも大きい`max_allowed_packet`の設定よりも大きなパケットを処理する別のタスクを実行する場合に発生する可能性のある、`var/log/exception.log`のデータベース接続エラーの解決策を紹介します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、すべて[ サポートされているバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## イシュー

[!DNL MySQL] クライアントまたは[mysqld](https://dev.mysql.com/doc/refman/8.0/en/mysqld.html) サーバーが[max\_allowed\_packet](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_max_allowed_packet) バイトを超えるパケットを受信すると、[ER\_NET\_PACKET\_TOO\_LARGE](https://dev.mysql.com/doc/mysql-errors/8.0/en/server-error-reference.html#error_er_net_packet_too_large) エラー（`exception.log`で確認できます）が発生し、接続が閉じます。 一部のクライアントでは、通信パケットが大きすぎる場合、クエリ *エラー中に* サーバーへの接続が失われる可能性があります。[!DNL MySQL]

<u>複製する手順</u>

さまざまなタスクがこの問題を引き起こす可能性があります。 これには、大量の商品をAdobe Commerceにインポートしようとしたり、トランザクションクエリで返されるデータが多すぎたりすることが含まれます。 その結果、`var/log/exception.log`のデータベース接続エラーと、製品が正常にインポートされないなど、その他の問題が発生します。

## 原因

[!DNL MySQL] `max_allowed_packets`設定のデフォルト値である16 MBは、必要に応じて十分なサイズではありません。

## Solution

1. 個々の行が現在の`max_allowed_packet`制限を超えているクエリを特定します。 このようなクエリは、返されるデータ量を減らすために書き換える必要があります。 これは、`SELECT` ステートメントの列数を減らすか、テーブルデザインの一部として、様々な列のデータタイプを小さく選択することで実行できます。 New Relic アカウントをお持ちの場合は、[New Relic APM Errors page](https://docs.newrelic.com/docs/apm/apm-ui-pages/error-analytics/errors-page-explore-events-behind-errors)および[New Relic APM Databases page](https://docs.newrelic.com/docs/apm/apm-ui-pages/monitoring/databases-page-view-operations-throughput-response-time)と[New Relic Logs](https://docs.newrelic.com/docs/logs/log-management/get-started/get-started-log-management)を使用して、関連するクエリを検索します。
1. 迅速な修復のために、[ チケットを送信するときに`max_allowed_packet` サイズを一時的に増やすようにリクエストできますが](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)、これはカスタマーエンジニアリングチームの裁量で行います。値が大きすぎると、ネットワークの混雑を引き起こしてレプリケーション障害が発生する可能性があるためです。
1. ベストプラクティスとして、一部の大規模なデータベーステーブルに対して、CLIで次のコマンドを実行する必要があります。

   ```
   show table status like [table name to match]
   ```

   これらのテーブルで実行されているクエリを評価して、推奨される`max_allowed_packet` サイズの16 MBを超えているかどうかを判断します。 同じ手順に従って、このようなクエリによって返されるデータを減らします。

## 関連トピックス

* 開発者向けドキュメントの[ オンプレミス インストールの概要](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview)。
* [ クラウドインフラストラクチャ上のAdobe Commerceのデータベースのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html)をサポートナレッジベースでご覧ください。
* [ データベースのパフォーマンスの問題を解決するためのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html)をサポートナレッジベースでご覧ください。
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
