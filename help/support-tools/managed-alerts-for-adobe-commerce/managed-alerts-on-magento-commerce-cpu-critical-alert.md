---
title: 「Adobe Commerceの管理アラート：CPU 重大なアラート」
description: この記事では、New RelicでAdobe Commerceの CPU クリティカルなアラートを受け取った場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 45b8ced0-b12f-428b-9838-2a9c26b9874b
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 5be8f2969426078bfcc0e4ffb4895dcf0327165f
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：CPU 重大なアラート

この記事では、New RelicでAdobe Commerceの CPU クリティカルなアラートを受け取った場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![disk critical アラート](assets/cpu-critical-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ

## 問題

にサインアップすると、New Relicで管理アラートが届きます。 [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) 1 つ以上のアラートしきい値を超えています。 これらのアラートは、サポートおよびエンジニアリングのインサイトを使用して、標準セットをお客様に提供するために、Adobe Commerceで開発されました。

<u>**動け！**</u>:

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、次を参照してください [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、次を参照してください [除外 IP アドレスの一覧を管理します](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten#instgde-cli-maint-exempt) 開発者向けドキュメントを参照してください。

<u>**止めて！**</u>:

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* インデクサーまたは追加のクローンを実行すると、CPU またはディスクに追加の負荷がかかる可能性があります。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

アラートの原因を調査して解決する前に「回避」アクションのいずれかを行った場合、（サイトの停止が発生していない場合は）サイトが応答しなくなる可能性があります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

>[!WARNING]
>
>これは重大なアラートなので、完了することを強くお勧めします **手順 1** 問題のトラブルシューティングを行う前に（手順 2 以降）。

Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、次を参照してください [サポートチケットのトラッキング](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) サポートナレッジベースで。 サポートは、New Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。

1. 連絡先の理由：「New Relicの重大なアラートを受信しました」を選択します。
1. アラートの説明。
1. [New Relic インシデント リンク](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents). これはに含まれています [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md).
1. 使用方法 [New Relic APM のトランザクションページ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) パフォーマンスの問題があるトランザクションを識別するには：
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 A [apdex スコアの低さ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-apdex-warning-alert.md) ボトルネック（応答時間の長いトランザクション）を示している場合があります。 通常、これはデータベース、Redis、または PHP に関連しています。 手順については、New Relicを参照してください。 [Apdex の不満が最も高いトランザクションの表示](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/view-your-apdex-score#apdex-dissat).
   * スループット、平均応答時間が遅い、時間がかかる、その他のしきい値の高い順にトランザクションを並べ替えます。 手順については、New Relicを参照してください。 [特定のパフォーマンスの問題を見つける](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems).
1. ソースの特定に苦労する場合は、を使用します [New Relic APM のインフラストラクチャページ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page) リソース負荷の高いサービスを特定する。 手順については、New Relicを参照してください。 [インフラストラクチャ監視ホスト・ページ/「プロセス」タブ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes).
1. ソースを特定した場合は、環境に SSH で接続して詳細を調べます。 手順については、次を参照してください [クラウドインフラストラクチャー上のAdobe Commerceを使用する場合は、環境に SSH で接続します。](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html) 開発者向けドキュメントを参照してください。
1. ソースの特定に苦労する場合：
   * 最近のトレンドを確認して、最近のコードのデプロイメントや設定の変更に関する問題を特定します（例えば、新しい顧客グループやカタログの大幅な変更）。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
   * フラットカタログの確認と無効化を検討します。 手順については、次を参照してください [パフォーマンスが遅く、動作が遅く、長時間実行されるクローン](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) サポートナレッジベースで。
   * DDoS 攻撃が発生していると思われる場合は、ボットトラフィックをブロックしてみてください。 手順については、次を参照してください [Fastly レベルでクラウドインフラストラクチャ上のAdobe Commerceの悪意のあるトラフィックをブロックする方法](/help/how-to/general/block-malicious-traffic-for-magento-commerce-on-fastly-level.md) サポートナレッジベースで。
1. 問題が一時的であると思われる場合は、アップサイズなどの軽減手順を実行するか、サイトをメンテナンスモードにします。 手順については、次を参照してください [一時サイズ変更のリクエスト方法](/help/how-to/general/how-to-request-temporary-magento-upsize.md) サポートナレッジベースおよび [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。 アップサイズによってサイトが通常の処理に戻った場合は、永続的なアップサイズを要求するか（Adobeアカウントチームに問い合わせてください）、負荷テストを実行してサービスの負荷を軽減するクエリまたはコードを最適化し、専用ステージングで問題を再現することを試みてください。 手順については、次を参照してください [テストデプロイメント/負荷テストとストレステスト](https://devdocs.magento.com/cloud/live/stage-prod-test.html#loadtest) （クラウドインフラストラクチャー上のAdobe Commerceに関する開発者向けドキュメント）を参照してください。
