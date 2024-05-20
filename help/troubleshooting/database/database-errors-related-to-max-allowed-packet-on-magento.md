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

この記事では、におけるデータベース接続エラーの解決策について説明します `var/log/exception.log` これは、多数の製品をインポートする場合や、で設定されているよりも大きなパケットをサーバーで強制的に処理する別のタスクを実行する場合に発生する可能性があります。 `max_allowed_packet` これは、デフォルトの 16 MB よりも大きいサイズです。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、すべて [サポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

MySQL クライアント [mysqld](https://dev.mysql.com/doc/refman/8.0/en/mysqld.html) サーバーがよりも大きいパケットを受信しました [max\_allowed\_packet](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_max_allowed_packet) バイト、問題あり [ER\_NET\_PACKET\_TOO\_LARGE](https://dev.mysql.com/doc/mysql-errors/8.0/en/server-error-reference.html#error_er_net_packet_too_large) エラー（以下で確認できます `exception.log`）を選択して、接続を閉じます。 一部のクライアントでは、 *クエリ中に MySQL サーバーへの接続が失われました* 通信パケットが大きすぎる場合のエラー。

<u>再現手順</u>

この問題は、様々なタスクが原因で発生する可能性があります。 これには、大量の商品をAdobe Commerceに読み込もうとすることや、大量のデータを送り返すトランザクションクエリなどが含まれます。 その結果、でデータベース接続エラーが発生します `var/log/exception.log` などの問題が発生します（製品が正常に読み込まれない）。

## 原因：

MySQL のデフォルト値は 16 MB です `max_allowed_packets` 設定は、ニーズに合わせて十分な大きさではありません。

## 解決策

1. 個々の行が現在の行を超えるクエリを特定する `max_allowed_packet` 制限。 返されるデータの量を減らすには、このようなクエリを書き換える必要があります。 これを行うには、の列数を少なくします `SELECT` テーブル設計の一環として、様々な列に対してステートメントを使用するか、より小さなデータ型を選択します。 New Relic アカウントがある場合は、 [New Relic APM エラーページ](https://docs.newrelic.com/docs/apm/apm-ui-pages/error-analytics/errors-page-explore-events-behind-errors) および [New Relic APM データベースページ](https://docs.newrelic.com/docs/apm/apm-ui-pages/monitoring/databases-page-view-operations-throughput-response-time)、および [New Relic ログ](https://docs.newrelic.com/docs/logs/log-management/get-started/get-started-log-management) 関連するクエリを検索できます。
1. 迅速な修正を行うために、を一時的にリクエストできます。 `max_allowed_packet` 次の場合にサイズを増やす [チケットの送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)ただし、値が大きすぎると、ネットワークの輻輳が発生してレプリケーションに失敗する可能性があるので、これはカスタマーエンジニアリングチームの判断です。
1. ベストプラクティスとして、一部の大規模なデータベーステーブルに対して、CLI で次のコマンドを実行する必要があります。

   ```
   show table status like [table name to match]
   ```

   これらのテーブルで実行されているクエリを評価して、推奨される制限を超えていないかどうかを判断します `max_allowed_packet` サイズは 16 MB です。 手順 1 と同じプロセスに従って、このようなクエリによって返されるデータを減らします。

## 関連資料

* [インストールガイド/MySQL](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/mysql.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=max%20allowed%2016%20MB) 開発者向けドキュメントを参照してください。
* [データベースのアップロードにより MySQL への接続が失われる](/help/troubleshooting/database/database-upload-loses-connection-to-mysql.md) サポートナレッジベースで。
* [クラウドインフラストラクチャー上のAdobe Commerceに関するデータベースのベストプラクティス](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html) サポートナレッジベースで。
* [データベースのパフォーマンスの問題を解決するベストプラクティス](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) サポートナレッジベースで。
