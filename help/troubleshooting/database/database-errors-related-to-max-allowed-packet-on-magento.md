---
title: Adobe Commerceの max_allowed_packet に関連するデータベースエラー
description: この記事では、多数の製品をインポートしたり、デフォルトの 16MB よりも大きい「max_allowed_packet」で設定されているサイズよりも大きいパケットをサーバーで強制的に処理する別のタスクを実行したりすると、「var/log/exception.log」で発生する可能性があるデータベース接続エラーの解決策を示します。
exl-id: e8932b72-91a3-43ea-800e-a6c7a5a17656
feature: Best Practices, Observability, Services
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Adobe Commerceの max_allowed_packet に関連するデータベースエラー

この記事では、多数の製品をインポートしたり、デフォルトの 16MB よりも大きい `max_allowed_packet` で設定されているサイズよりも大きいパケットをサーバーで強制的に処理する別のタスクを実行したりしたときに発生する可能性がある `var/log/exception.log` ータのデータベース接続エラーに対する解決策を示します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、すべて [ サポート対象バージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

MySQL クライアントまたは [mysqld](https://dev.mysql.com/doc/refman/8.0/en/mysqld.html) サーバーが [max\_allowed\_packet](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_max_allowed_packet) バイトを超えるパケットを受信すると、[ER\_NET\_PACKET\_TOO\_LARGE](https://dev.mysql.com/doc/mysql-errors/8.0/en/server-error-reference.html#error_er_net_packet_too_large) エラー（`exception.log` に表示されます）を発行して接続を閉じます。 一部のクライアントでは、通信パケットが大きすぎると、*クエリ中に MySQL サーバーへの接続が失われる* というエラーが発生する場合があります。

<u> 再現手順 </u>

この問題は、様々なタスクが原因で発生する可能性があります。 これには、大量の商品をAdobe Commerceに読み込もうとすることや、大量のデータを送り返すトランザクションクエリなどが含まれます。 その結果、`var/log/exception.log` でデータベース接続エラーが発生し、製品が正常に読み込まれないなどの問題が発生します。

## 原因：

MySQL `max_allowed_packets` 設定のデフォルト値 16MB は、ニーズに合った大きさではありません。

## 解決策

1. 個々の行が現在の `max_allowed_packet` 制限を超えているクエリを特定します。 返されるデータの量を減らすには、このようなクエリを書き換える必要があります。 これは、`SELECT` ステートメントの列数を減らすか、テーブルデザインの一環として様々な列に対して小さいデータ型を選択することで行うことができます。 New Relic アカウントをお持ちの場合、[New Relic APM Errors ページ ](https://docs.newrelic.com/docs/apm/apm-ui-pages/error-analytics/errors-page-explore-events-behind-errors)[New Relic APM Databases ページ ](https://docs.newrelic.com/docs/apm/apm-ui-pages/monitoring/databases-page-view-operations-throughput-response-time) および [New Relic Logs](https://docs.newrelic.com/docs/logs/log-management/get-started/get-started-log-management) を使用して、関連するクエリを検索します。
1. 迅速な修復を行うために、[ チケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) する際に、`max_allowed_packet` のサイズを増やすように一時的にリクエストできますが、値が大きすぎると、ネットワークの輻輳が発生してレプリケーションにエラーが発生する可能性があるので、これはカスタマー・エンジニアリング・チームの判断で行います。
1. ベストプラクティスとして、一部の大規模なデータベーステーブルに対して、CLI で次のコマンドを実行する必要があります。

   ```
   show table status like [table name to match]
   ```

   これらのテーブルで実行されているクエリを評価して、推奨される `max_allowed_packet` サイズを 16 MB 超えていないかどうかを判断します。 手順 1 と同じプロセスに従って、このようなクエリによって返されるデータを減らします。

## 関連資料

* 開発者向けドキュメントの [ インストールガイド/MySQL](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/mysql.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=max%20allowed%2016%20MB)。
* サポートナレッジベースの [ データベースのアップロードにより、MySQL への接続が失われます ](/help/troubleshooting/database/database-upload-loses-connection-to-mysql.md)。
* [ クラウドインフラストラクチャー上のAdobe Commerceに関するデータベースのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html) については、サポートナレッジベースを参照してください。
* サポートナレッジベースの [ データベースパフォーマンスの問題を解決するためのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html)。
