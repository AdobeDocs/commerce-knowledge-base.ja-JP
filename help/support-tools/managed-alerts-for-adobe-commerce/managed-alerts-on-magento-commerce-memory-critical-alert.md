---
title: 「Adobe Commerceの管理アラート：メモリクリティカルアラート」
description: この記事では、New RelicでAdobe Commerceのメモリクリティカルアラートを受け取った場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: feed7998-c50b-4cbf-a92d-cbfc65745a1c
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 468ad1c47da3c299b8028726e79e25a4aa9489ea
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：メモリ障害アラート

この記事では、New RelicでAdobe Commerceのメモリクリティカルアラートを受け取った場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![disk critical アラート](assets/memory-critical-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce Pro のすべてのバージョンは、アーキテクチャを計画します。

## 問題

にサインアップすると、New Relicで管理アラートが届きます。 [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) 1 つ以上のアラートしきい値を超えています。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

<u> **動け！** </u>

* このアラートがクリアされるまでスケジュールされている展開を中止する
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、を参照してください [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、を参照してください [除外 IP アドレスの一覧を管理します](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten#instgde-cli-maint-exempt) 開発者向けドキュメントを参照してください。

<u>**止めて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

アラートの原因を調査して解決する前に「回避」アクションのいずれかを行った場合、（まだサイトの停止が発生していない場合は）サイトが応答しなくなる可能性があります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

>[!WARNING]
>
>これは重大なアラートなので、完了することを強くお勧めします **手順 1** 問題のトラブルシューティングを行う前に（手順 2 以降）。

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、を参照してください [サポートチケットのトラッキング](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) サポートナレッジベースで。 サポートは、既にNew Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。
   * 連絡先理由：「New Relicの重大なアラートを受信しました」を選択します
   * アラートの説明
   * [New Relic インシデント リンク](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents). これはに含まれています [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md).

1. 使用方法 [New Relic APM のインフラストラクチャページ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) 大量のメモリを消費する上位のプロセスを特定します。 手順については、New Relicを参照してください。 [インフラストラクチャ監視ホスト・ページ/「プロセス」タブ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes):
   * Redis、MySQL、PHP などのサービスがメモリ消費の上位ソースである場合は、次の操作を実行してください。
1. 最新バージョンを使用していることを確認します。 新しいバージョンでは、メモリリークが修正される場合があります。 最新バージョンでない場合は、アップグレードを検討してください。 手順については、次を参照してください [クラウドインフラストラクチャー上のAdobe Commerce/サービス/サービスを変更](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) 開発者向けドキュメントを参照してください。
1. サービスの問題がバージョンに関連したものでない場合は、次の操作を試してください。
1. **MySQL**：クエリの長時間実行、プライマリキーが定義されていない、インデックスが重複しているなどの問題がないか確認します。 手順については、次を参照してください [クラウドインフラストラクチャー上のAdobe Commerceにおけるデータベースの最も一般的な問題](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) サポートナレッジベースで。
1. **Redis**:Redis がメモリ消費の上位ソースの場合、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).
1. **PHP**:PHP がメモリ消費の上位ソースの場合、を実行して実行中のプロセスを確認します `ps aufx` CLI/ターミナルで実行します。 ターミナル出力には、現在実行中の cron ジョブとプロセスが表示されます。 出力でプロセスの実行時間を確認します。 実行時間が長い Cron がある場合は、Cron がハングしている可能性があります。 トラブルシューティング手順については、を参照してください。 [パフォーマンスが遅く、動作が遅く、長時間実行されるクローン](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) および [Cron ジョブが「実行中」ステータスでスタックしました](https://support.magento.com/hc/en-us/articles/360033099451) サポートナレッジベースで。
1. それでも問題の原因を特定できない場合は、次を使用します [New Relic APM のトランザクションページ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) パフォーマンスの問題があるトランザクションを識別するには：
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 A [apdex スコアの低さ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-apdex-warning-alert.md) ボトルネック（応答時間の長いトランザクション）を示している場合があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relicを参照してください。 [Apdex の不満が最も高いトランザクションの表示](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/view-your-apdex-score#apdex-dissat).
   * スループット、平均応答時間が最も遅い、最も時間がかかる、およびその他のしきい値でトランザクションを並べ替えます。 手順については、New Relicを参照してください。 [特定のパフォーマンスの問題を見つける](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems). それでも問題を特定できない場合は、New Relic APM の「インフラストラクチャ」ページを使用します。
1. メモリ消費が増加した原因を特定できない場合は、最近の傾向を確認して、最近のコードのデプロイメントまたは設定の変更に関する問題（新しい顧客グループやカタログの大幅な変更など）を特定します。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. 上記の方法で適切な時間内に原因や解決策を見つけることができない場合は、アップサイズをリクエストするか、まだサイトをメンテナンスモードに設定していない場合は、サイトをメンテナンスモードに設定します。 手順については、を参照してください [一時サイズ変更のリクエスト方法](/help/how-to/general/how-to-request-temporary-magento-upsize.md) サポートナレッジベース [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。
1. アップサイズによってサイトが通常の処理に戻った場合は、永続的なアップサイズを要求するか（Adobeアカウントチームにお問い合わせください）、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用のステージングで問題を再現することを試みてください。 参照： [クラウドインフラストラクチャー上のAdobe Commerce/テストデプロイメント/負荷テストとストレステスト](https://devdocs.magento.com/cloud/live/stage-prod-test.html#loadtest) 開発者向けドキュメントを参照してください。
