---
title: 「Adobe Commerceの管理アラート：Apdex 重大アラート」
description: この記事では、New RelicでAdobe Commerceに関する Apdex の重要なアラートを受け取った場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: b6d3d4f3-4abb-4285-8071-2b9fb06bfa3c
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: fbb24fb3c8b399f3b7e19c663eb4b168657498e6
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：Apdex 重大アラート

この記事では、New RelicでAdobe Commerceに関する Apdex の重要なアラートを受け取った場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![apdex 重大アラート](assets/apdex-critical-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ
* Adobe Commerce on cloud infrastructure スタータープランアーキテクチャ

## 問題

にサインアップすると、New Relicで管理アラートが届きます。 [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) 1 つ以上のアラートしきい値を超えています。 これらのアラートは、マーチャントがサポートとエンジニアリングのインサイトを使用して標準セットを提供するために、Adobeによって開発されました。

<u> **動け！** </u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、次を参照してください [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、次を参照してください [除外 IP アドレスの一覧を管理します](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten#instgde-cli-maint-exempt) 開発者向けドキュメントを参照してください。

<u>**止めて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

アラートの原因をトラブルシューティングする前に、重要なアラートを受け取ったときに上記の手順を実行すると、まだサイトの停止が発生していない場合、サイトが応答しなくなります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

>[!WARNING]
>
>これは重大なアラートなので、完了することを強くお勧めします **手順 1** 問題のトラブルシューティングを行う前に（手順 2 以降）。

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、次を参照してください [サポートチケットのトラッキング](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) サポートナレッジベースで。 サポートは、New Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。
   * 連絡先の理由：「New Relicの重大なアラートを受信しました」を選択します。
   * アラートの説明。
   * [New Relic インシデント リンク](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents). これはに含まれています [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md).
1. 問題の原因を特定するには、次を使用します [New Relic APM のトランザクションページ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) パフォーマンスの問題があるトランザクションを識別するには：
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 Apdex スコアが低い場合、ボトルネック（応答時間の長いトランザクション）を示している可能性があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relicを参照してください。 [Apdex の不満が最も高いトランザクションの表示](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/#dissatisfaction).
   * スループット、平均応答時間が最も遅い、最も時間がかかる、およびその他のしきい値でトランザクションを並べ替えます。 手順については、New Relicを参照してください。 [特定のパフォーマンスの問題を見つける](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems). それでも問題を特定できない場合は、New Relic APM の「インフラストラクチャ」ページを使用します。
1. 使用方法 [New Relic APM のインフラストラクチャページ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) 大量のリソースを消費するプロセスを特定する。 手順については、New Relicを参照してください。 [インフラストラクチャ監視ホスト・ページ/「プロセス」タブ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes).
1. メモリ消費の上位ソースが Redis や MySQL などのサービスである場合は、次の操作を実行してください。
   * 最新バージョンを使用していることを確認します。 新しいバージョンでは、メモリリークが修正される場合があります。 最新バージョンでない場合は、アップグレードを検討してください。 手順については、次を参照してください [Cloud for Adobe Commerce/サービス/サービスを変更](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) 開発者向けドキュメントを参照してください。
   * 長時間実行中のクエリ、プライマリキーが定義されていない、インデックスが重複しているなど、MySQL の問題を確認します。 手順については、次を参照してください [クラウドインフラストラクチャー上のAdobe Commerceにおけるデータベースの最も一般的な問題](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) 開発者向けドキュメントを参照してください。
   * PHP の問題をチェックします。 を実行して実行中のプロセスを確認する `ps aufx` CLI/ターミナルで実行します。 ターミナル出力には、現在実行中の cron ジョブとプロセスが表示されます。 出力でプロセスの実行時間を確認します。 実行時間が長い Cron がある場合は、Cron がハングしている可能性があります。 トラブルシューティング手順については、を参照してください。 [パフォーマンスが遅く、動作が遅く、長時間実行されるクローン](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) および [Cron ジョブが「実行中」ステータスでスタックしました](/help/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.md) サポートナレッジベースで。

1. ソースが特定されたら、環境に SSH で接続して詳細を調べます。 手順については、次を参照してください [Cloud for Adobe Commerce/技術と要件/お使いの環境への SSH](https://devdocs.magento.com/cloud/env/environments-ssh.html#ssh) 開発者向けドキュメントを参照してください。
1. ソースの特定に引き続き苦労する場合は、最近のトレンドを確認し、最近のコードのデプロイメントまたは設定の変更に関する問題を特定します（例えば、新しい顧客グループやカタログの大幅な変更）。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. 妥当な時間内にソリューションが見つからない場合は、アップサイズをリクエストするか、サイトをまだメンテナンスモードに設定していない場合は配置します。 手順については、次を参照してください [一時サイズ変更のリクエスト方法](/help/how-to/general/how-to-request-temporary-magento-upsize.md) サポートナレッジベース [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。
1. アップサイズによってサイトが通常の処理に戻った場合は、永続的なアップサイズを要求するか（Adobeアカウントチームにお問い合わせください）、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用のステージングで問題を再現することを試みてください。 こちらを参照してください [Cloud for Adobe Commerce/テストデプロイメント/負荷テストとストレステスト](https://devdocs.magento.com/cloud/live/stage-prod-test.html#loadtest) 開発者向けドキュメントを参照してください。
