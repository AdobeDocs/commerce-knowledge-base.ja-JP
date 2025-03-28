---
title: 「Adobe Commerceの管理アラート：Apdex 重大アラート」
description: この記事では、New RelicでAdobe Commerceに関する Apdex の重要なアラートを受け取った場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: b6d3d4f3-4abb-4285-8071-2b9fb06bfa3c
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：Apdex 重大アラート

この記事では、New RelicでAdobe Commerceに関する Apdex の重要なアラートを受け取った場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![apdex 重大アラート ](assets/apdex-critical-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ
* Adobe Commerce on cloud infrastructure スタータープランアーキテクチャ

## 問題

[Adobe Commerceの管理アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicで管理アラートを受け取ります。 これらのアラートは、マーチャントがサポートとエンジニアリングのインサイトを使用して標準セットを提供するために、Adobeによって開発されました。

<u> **動け！**</u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、開発者向けドキュメントの [ 免除 IP アドレスのリストを管理する ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode#instgde-cli-maint-exempt) を参照してください。

<u>**やめて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

アラートの原因をトラブルシューティングする前に、重要なアラートを受け取ったときに上記の手順を実行すると、まだサイトの停止が発生していない場合、サイトが応答しなくなります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

>[!WARNING]
>
>これは重大なアラートなので、問題のトラブルシューティング（手順 2 以降）を行う前に、**手順 1** を完了することを強くお勧めします。

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、サポートナレッジベースの [ サポートチケットの追跡 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) を参照してください。 サポートは、New Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。
   * 連絡先の理由：「New Relicの重大なアラートを受信しました」を選択します。
   * アラートの説明。
   * [New Relic インシデントのリンク ](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents)。 これは、[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) に含まれています。
1. 問題の原因を特定するには、[New Relic APM のトランザクションページ ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を使用して、パフォーマンスの問題があるトランザクションを特定します。
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) は、web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 Apdex スコアが低い場合、ボトルネック（応答時間の長いトランザクション）を示している可能性があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relic[Apdex の不満が最も高いトランザクションの表示 ](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/#dissatisfaction) を参照してください。
   * スループット、平均応答時間が最も遅い、最も時間がかかる、およびその他のしきい値でトランザクションを並べ替えます。 手順については、New Relic[ 特定のパフォーマンスの問題の検索 ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を参照してください。 それでも問題を特定できない場合は、New Relic APM の「インフラストラクチャ」ページを使用します。
1. [New Relic APM のインフラストラクチャページ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) を使用して、リソースを大量に消費するプロセスを特定します。 手順については、New Relicを参照してください [Infrastructure monitoring Hosts ページ/「プロセス」タブ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes)。
1. メモリ消費の上位ソースが Redis や MySQL などのサービスである場合は、次の操作を実行してください。
   * 最新バージョンを使用していることを確認します。 新しいバージョンでは、メモリリークが修正される場合があります。 最新バージョンでない場合は、アップグレードを検討してください。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/サービス/サービスを変更 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) を参照してください。
   * 長時間実行中のクエリ、プライマリキーが定義されていない、インデックスが重複しているなど、MySQL の問題を確認します。 手順については、開発者向けドキュメントの [ クラウドインフラストラクチャ上のAdobe Commerceで最も一般的なデータベースの問題 ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) を参照してください。
   * PHP の問題をチェックします。 CLI/ターミナルで `ps aufx` を実行して、実行中のプロセスを確認します。 ターミナル出力には、現在実行中の cron ジョブとプロセスが表示されます。 出力でプロセスの実行時間を確認します。 実行時間が長い Cron がある場合は、Cron がハングしている可能性があります。 トラブルシューティングの手順については、サポートナレッジベースの [ パフォーマンスが遅い、実行時間が長い、Cron](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) および [Cron ジョブが「実行中」ステータスのままになる ](/help/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.md) を参照してください。

1. ソースが特定されたら、環境に SSH で接続して詳細を調べます。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/技術と要件/SSH](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh) を参照してください。
1. ソースの特定に引き続き苦労する場合は、最近のトレンドを確認し、最近のコードのデプロイメントまたは設定の変更に関する問題を特定します（例えば、新しい顧客グループやカタログの大幅な変更）。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. 妥当な時間内にソリューションが見つからない場合は、アップサイズをリクエストするか、サイトをまだメンテナンスモードに設定していない場合は配置します。 手順については、サポートナレッジベースの [temp resize のリクエスト方法 ](/help/how-to/general/how-to-request-temporary-magento-upsize.md) および開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。
1. アップサイズによってサイトが通常の処理に戻った場合は、永続的なアップサイズを要求するか（Adobeアカウントチームにお問い合わせください）、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用のステージングで問題を再現することを試みてください。 開発者向けドキュメントの [Cloud for Adobe Commerce/テストデプロイメント/負荷とストレステスト ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production#load-and-stress-testing) を参照してください。
