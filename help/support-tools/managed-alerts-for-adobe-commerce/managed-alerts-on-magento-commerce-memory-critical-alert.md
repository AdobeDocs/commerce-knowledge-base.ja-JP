---
title: 「Adobe Commerceの管理アラート：メモリクリティカルアラート」
description: この記事では、New RelicでAdobe Commerceのメモリクリティカルアラートを受け取った場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: feed7998-c50b-4cbf-a92d-cbfc65745a1c
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：メモリ障害アラート

この記事では、New RelicでAdobe Commerceのメモリクリティカルアラートを受け取った場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![disk critical アラート ](assets/memory-critical-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce Pro のすべてのバージョンは、アーキテクチャを計画します。

## 問題

[Adobe Commerceの管理アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicで管理アラートを受け取ります。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

<u> **動け！**</u>

* このアラートがクリアされるまでスケジュールされている展開を中止する
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、開発者向けドキュメントの [ 免除 IP アドレスのリストを維持する ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode#instgde-cli-maint-exempt) を参照してください。

<u>**やめて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

アラートの原因を調査して解決する前に「回避」アクションのいずれかを行った場合、（まだサイトの停止が発生していない場合は）サイトが応答しなくなる可能性があります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

>[!WARNING]
>
>これは重大なアラートなので、問題のトラブルシューティング（手順 2 以降）を行う前に、**手順 1** を完了することを強くお勧めします。

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、サポートナレッジベースの [ サポートチケットのトラッキング ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) を参照してください。 サポートは、既にNew Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。
   * 連絡先理由：「New Relicの重大なアラートを受信しました」を選択します
   * アラートの説明
   * [New Relic インシデントのリンク ](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents)。 これは、[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) に含まれています。

1. [New Relic APM のインフラストラクチャページ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) を使用して、メモリを大量に消費する上位のプロセスを特定します。 手順については、New Relicを参照してください [ インフラストラクチャの監視ホスト ページ/「プロセス」タブ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes)。
   * Redis、MySQL、PHP などのサービスがメモリ消費の上位ソースである場合は、次の操作を実行してください。
1. 最新バージョンを使用していることを確認します。 新しいバージョンでは、メモリリークが修正される場合があります。 最新バージョンでない場合は、アップグレードを検討してください。 手順については、開発者向けドキュメントの [ クラウドインフラストラクチャー上のAdobe Commerce/サービス/サービスを変更 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) を参照してください。
1. サービスの問題がバージョンに関連したものでない場合は、次の操作を試してください。
1. **MySQL**：クエリの長時間実行、プライマリキーが定義されていない、インデックスが重複しているなどの問題がないか確認してください。 手順については、サポートナレッジベースの [ クラウドインフラストラクチャ上のAdobe Commerceで発生するデータベースの最も一般的な問題 ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) を参照してください。
1. **Redis**:Redis がメモリ消費のトップソースの場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。
1. **PHP**: PHP がメモリ消費の上位のソースである場合は、CLI/ターミナルで `ps aufx` を実行して、実行中のプロセスを確認します。 ターミナル出力には、現在実行中の cron ジョブとプロセスが表示されます。 出力でプロセスの実行時間を確認します。 実行時間が長い Cron がある場合は、Cron がハングしている可能性があります。 トラブルシューティングの手順については、サポートナレッジベースの [ パフォーマンスが遅い、動作が遅い、動作が長い ](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) および [Cron ジョブが「実行中」ステータスのままになる ](https://support.magento.com/hc/en-us/articles/360033099451) を参照してください。
1. それでも問題の原因を特定できない場合は、[New Relic APM のトランザクションページ ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を使用して、パフォーマンスの問題があるトランザクションを特定します。
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) は、web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 [Apdex スコアが低い ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-apdex-warning-alert.md) は、ボトルネック（応答時間の長いトランザクション）を示している場合があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relic[Apdex の不満が最も高いトランザクションの表示 ](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/view-your-apdex-score#apdex-dissat) を参照してください。
   * スループット、平均応答時間が最も遅い、最も時間がかかる、およびその他のしきい値でトランザクションを並べ替えます。 手順については、New Relic[ 特定のパフォーマンスの問題の検索 ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を参照してください。 それでも問題を特定できない場合は、New Relic APM の「インフラストラクチャ」ページを使用します。
1. メモリ消費が増加した原因を特定できない場合は、最近の傾向を確認して、最近のコードのデプロイメントまたは設定の変更に関する問題（新しい顧客グループやカタログの大幅な変更など）を特定します。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. 上記の方法で適切な時間内に原因や解決策を見つけることができない場合は、アップサイズをリクエストするか、まだサイトをメンテナンスモードに設定していない場合は、サイトをメンテナンスモードに設定します。 手順については、サポートナレッジベースの [ 一時サイズ変更のリクエスト方法 ](/help/how-to/general/how-to-request-temporary-magento-upsize.md) および開発者ドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。
1. アップサイズによってサイトが通常の処理に戻った場合は、永続的なアップサイズを要求するか（Adobeアカウントチームにお問い合わせください）、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用のステージングで問題を再現することを試みてください。 開発者向けドキュメントの [ クラウドインフラストラクチャー上のAdobe Commerce/テストデプロイメント/負荷およびストレステスト ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production#load-and-stress-testing) を参照してください。
