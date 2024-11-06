---
title: 「Adobe Commerceの管理アラート：Apdex 警告アラート」
description: この記事では、New RelicでAdobe Commerceに関する Apdex 警告アラートが表示された場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 6e3f28ae-734b-468f-b6a5-c4f2edb1cb4b
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：Apdex 警告アラート

この記事では、New RelicでAdobe Commerceに関する Apdex 警告アラートが表示された場合のトラブルシューティング手順を説明します。 Apdex スコアは、web アプリケーションおよびサービスの応答時間に対するユーザーの満足度を測定します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![apdex 警告アラート ](assets/apdex-warning-magento-managed.png){width="500"}

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

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

1. 問題の原因を特定するには、[New Relic APM のトランザクションページ ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を使用して、パフォーマンスの問題があるトランザクションを特定します。
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) は、web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 [Apdex スコアが低い ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-apdex-warning-alert.md) は、ボトルネック（応答時間の長いトランザクション）を示している場合があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relic[Apdex の不満が最も高いトランザクションの表示 ](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/view-your-apdex-score#apdex-dissat) を参照してください。
   * スループット、平均応答時間が最も遅い、最も時間がかかる、およびその他のしきい値でトランザクションを並べ替えます。 手順については、New Relic[ 特定のパフォーマンスの問題の検索 ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を参照してください。
1. [New Relic APM のインフラストラクチャページ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) を使用して、リソースを大量に消費するプロセスを特定します。 手順については、New Relicを参照してください [Infrastructure monitoring Hosts ページ/「プロセス」タブ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes)。
1. メモリ消費の上位ソースが Redis や MySQL などのサービスである場合は、次の操作を実行してください。
   * 最新バージョンを使用していることを確認します。 新しいバージョンでは、メモリリークが修正される場合があります。 最新バージョンでない場合は、アップグレードを検討してください。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/サービス/サービスを変更 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) を参照してください。
1. 問題がサービスのバージョンに起因するものではない場合：
   * 長時間実行中のクエリ、プライマリキーが定義されていない、インデックスが重複しているなど、MySQL のその他の問題を確認します。 手順については、サポートナレッジベースの [ クラウドインフラストラクチャ上のAdobe Commerceで発生するデータベースの最も一般的な問題 ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) を参照してください。
   * その他の PHP の問題をチェックします。 CLI/ターミナルで `ps aufx` を実行して、実行中のプロセスを確認します。 ターミナル出力には、現在実行中の cron ジョブとプロセスが表示されます。 出力でプロセスの実行時間を確認します。 実行時間が長い Cron がある場合は、Cron がハングしている可能性があります。 トラブルシューティングの手順については、サポートナレッジベースの [ パフォーマンスが遅い、実行時間が長い、Cron](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) および [Cron ジョブが「実行中」ステータスのままになる ](/help/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.md) を参照してください。
1. 問題の潜在的な原因が特定されたら、環境に SSH で問い合わせて詳細を確認します。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/技術と要件/SSH](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh) を参照してください。
1. ソースの特定に引き続き苦労する場合は、最近のトレンドを確認し、最近のコードのデプロイメントまたは設定の変更に関する問題を特定します（例えば、新しい顧客グループやカタログの大幅な変更）。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. 妥当な時間内にソリューションが見つからない場合は、アップサイズをリクエストするか、サイトをまだメンテナンスモードに設定していない場合は配置します。 手順については、サポートナレッジベースの [temp resize のリクエスト方法 ](/help/how-to/general/how-to-request-temporary-magento-upsize.md) および開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。
1. [upsize](/help/how-to/general/how-to-request-temporary-magento-upsize.md) によってサイトが通常の処理に戻った場合は、恒久的なアップサイズを要求すること（Adobeアカウントチームに連絡）を検討するか、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用ステージングで問題を再現することを試みます。 開発者向けドキュメントの [Cloud for Adobe Commerce/テストデプロイメント/負荷とストレステスト ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production#load-and-stress-testing) を参照してください。
