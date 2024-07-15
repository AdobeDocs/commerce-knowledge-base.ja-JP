---
title: 「Adobe Commerceの管理アラート：CPU 警告アラート」
description: この記事では、New RelicでAdobe Commerceの CPU 警告アラートが表示された場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 03686684-3b7e-430a-a05a-a96f38345322
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 324cce66df1e4ab7ec4ef8fb6512c3acbabdf3ab
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：CPU 警告アラート

この記事では、New RelicでAdobe Commerceの CPU 警告アラートが表示された場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![CPU 警告アラート ](assets/cpu-warning-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ

## 問題

[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicでアラートが届きます。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

<u> **動け！**</u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが完全に応答しない場合は、すぐにサイトをメンテナンスモードにします。 手順については、開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、開発者向けドキュメントの [ 免除 IP アドレスのリストを管理する ](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten#instgde-cli-maint-exempt) を参照してください。

<u>**やめて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

1. [New Relic APM のトランザクションページ ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を使用して、パフォーマンスの問題があるトランザクションを特定します。
   * Apdex スコアの昇順でトランザクションを並べ替えます。 [Apdex](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction) は、web アプリケーションおよびサービスの応答時間に対するユーザー満足度を指します。 [Apdex スコアが低い ](/help/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.md#low_user_satisfaction) は、ボトルネック（応答時間の長いトランザクション）を示している場合があります。 通常は、データベース、Redis、または PHP です。 手順については、New Relic[Apdex の不満が最も高いトランザクションの表示 ](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/view-your-apdex-score#apdex-dissat) を参照してください。
   * スループット、平均応答時間が遅い、時間がかかる、その他のしきい値の高い順にトランザクションを並べ替えます。 手順については、New Relic[ 特定のパフォーマンスの問題の検索 ](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/transactions-page-find-specific-performance-problems) を参照してください。
1. ソースの特定に苦労している場合は、[New Relic APM のインフラストラクチャページ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) を使用して、リソース負荷の高いサービスを特定します。 手順については、New Relicを参照してください [Infrastructure monitoring Hosts ページ/「プロセス」タブ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#processes)。
1. ソースを特定した場合は、環境に SSH で接続して詳細を調べます。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/SSH](https://devdocs.magento.com/cloud/env/environments-ssh.html#ssh) を参照してください。
1. ソースの特定に苦労する場合：
   * 最近のトレンドを確認して、最近のコードのデプロイメントや設定の変更に関する問題を特定します（例えば、新しい顧客グループやカタログの大幅な変更）。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
   * フラットカタログの確認と無効化を検討します。 手順については、サポートナレッジベースの [ パフォーマンスが遅い、動作が遅い、動作が長い ](/help/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.md) を参照してください。
   * DDoS 攻撃が発生していると思われる場合は、ボットトラフィックをブロックしてみてください。 手順については、サポートナレッジベースの [Fastly レベルでAdobe Commerceの悪意のあるトラフィックをブロックする方法 ](/help/how-to/general/block-malicious-traffic-for-magento-commerce-on-fastly-level.md) を参照してください。
1. 問題が一時的であると思われる場合は、アップサイズなどの軽減手順を実行するか、サイトをメンテナンスモードにします。 手順については、サポートナレッジベースの [temp resize のリクエスト方法 ](/help/how-to/general/how-to-request-temporary-magento-upsize.md) および開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) を参照してください。 アップサイズによってサイトが通常の処理に戻った場合は、永続的なアップサイズをリクエストするか（Adobeアカウントチームにお問い合わせください）、負荷テストを実行してクエリまたはサービスの負荷を軽減するコードを最適化し、専用のステージングで問題を再現することを試みてください。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/テストデプロイメント/負荷とストレステスト ](https://devdocs.magento.com/cloud/live/stage-prod-test.html#loadtest) を参照してください。
