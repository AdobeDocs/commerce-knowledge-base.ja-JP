---
title: 「Adobe Commerceの管理アラート：Apdex 警告アラート」
description: この記事では、New RelicでAdobe Commerceに関する Apdex 警告アラートが表示された場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 6e3f28ae-734b-468f-b6a5-c4f2edb1cb4b
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：Apdex 警告アラート

この記事では、New RelicでAdobe Commerceに関する Apdex 警告アラートが表示された場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![apdex 警告アラート](assets/apdex-warning-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ
* Adobe Commerce on cloud infrastructure スタータープランアーキテクチャ

## 問題

にサインアップすると、New Relicで管理アラートが届きます。 [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) 1 つ以上のアラートしきい値を超えています。 これらのアラートは、マーチャントがサポートとエンジニアリングのインサイトを使用して標準セットを提供するために、Adobeによって開発されました。

<u> **動け！** </u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、次を参照してください  [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、次を参照してください [除外 IP アドレスの一覧を管理します](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten#instgde-cli-maint-exempt) 開発者向けドキュメントを参照してください。

<u>**止めて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

1. 問題の原因を特定するには、次を使用します [New Relic APM のトランザクションページ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) パフォーマンスの問題があるトランザクションを識別するには：
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 A [apdex スコアの低さ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-apdex-warning-alert.md) ボトルネック（応答時間の長いトランザクション）を示している場合があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relicを参照してください。 [Apdex の不満が最も高いトランザクションの表示](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/view-your-apdex-score#apdex-dissat).
   * スループット、平均応答時間が最も遅い、最も時間がかかる、およびその他のしきい値でトランザクションを並べ替えます。 手順については、New Relicを参照してください。 [特定のパフォーマンスの問題を見つける](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems).
1. 使用方法 [New Relic APM のインフラストラクチャページ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) 大量のリソースを消費するプロセスを特定する。 手順については、New Relicを参照してください。 [インフラストラクチャ監視ホスト・ページ/「プロセス」タブ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes).
1. メモリ消費の上位ソースが Redis や MySQL などのサービスである場合は、次の操作を実行してください。
   * 最新バージョンを使用していることを確認します。 新しいバージョンでは、メモリリークが修正される場合があります。 最新バージョンでない場合は、アップグレードを検討してください。 手順については、次を参照してください [Cloud for Adobe Commerce/サービス/サービスを変更](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) 開発者向けドキュメントを参照してください。
1. 問題がサービスのバージョンに起因するものではない場合：
   * 長時間実行中のクエリ、プライマリキーが定義されていない、インデックスが重複しているなど、MySQL のその他の問題を確認します。 手順については、次を参照してください [クラウドインフラストラクチャー上のAdobe Commerceにおけるデータベースの最も一般的な問題](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) サポートナレッジベースで。
   * その他の PHP の問題をチェックします。 を実行して実行中のプロセスを確認する `ps aufx` CLI/ターミナルで実行します。 ターミナル出力には、現在実行中の cron ジョブとプロセスが表示されます。 出力でプロセスの実行時間を確認します。 実行時間が長い Cron がある場合は、Cron がハングしている可能性があります。 トラブルシューティング手順については、を参照してください。 [パフォーマンスが遅く、動作が遅く、長時間実行されるクローン](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) および [Cron ジョブが「実行中」ステータスでスタックしました](/help/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.md) サポートナレッジベースで。
1. 問題の潜在的な原因が特定されたら、環境に SSH で問い合わせて詳細を確認します。 手順については、次を参照してください [Cloud for Adobe Commerce/技術と要件/お使いの環境への SSH](https://devdocs.magento.com/cloud/env/environments-ssh.html#ssh) 開発者向けドキュメントを参照してください。
1. ソースの特定に引き続き苦労する場合は、最近のトレンドを確認し、最近のコードのデプロイメントまたは設定の変更に関する問題を特定します（例えば、新しい顧客グループやカタログの大幅な変更）。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. 妥当な時間内にソリューションが見つからない場合は、アップサイズをリクエストするか、サイトをまだメンテナンスモードに設定していない場合は配置します。 手順については、次を参照してください [一時サイズ変更のリクエスト方法](/help/how-to/general/how-to-request-temporary-magento-upsize.md) サポートナレッジベース [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。
1. 次の場合 [upsize](/help/how-to/general/how-to-request-temporary-magento-upsize.md) サイトを通常の処理に戻すか、永続的なアップサイズをリクエストすることを検討します（Adobeアカウントチームにお問い合わせください）。または、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用ステージングで問題を再現してみます。 こちらを参照してください [Cloud for Adobe Commerce/テストデプロイメント/負荷テストとストレステスト](https://devdocs.magento.com/cloud/live/stage-prod-test.html#loadtest) 開発者向けドキュメントを参照してください。
