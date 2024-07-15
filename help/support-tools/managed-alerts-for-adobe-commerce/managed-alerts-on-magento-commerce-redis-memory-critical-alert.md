---
title: 「Adobe Commerceの管理アラート：Redis メモリクリティカルアラート」
description: この記事では、New RelicのAdobe Commerceで Redis メモリクリティカルアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を解決するには、早急な対応が必要です。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 28e1d879-d7ca-4439-8e81-52a1fbf3ecb0
feature: Cache, Categories, Observability, Services, Support, Tools and External Services, Variables
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：Redis メモリクリティカルアラート

この記事では、New RelicのAdobe Commerceで Redis メモリクリティカルアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を解決するには、早急な対応が必要です。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![new_relic_redis_memory_critical.png](assets/new_relic_redis_memory_critical.png)

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャのすべてのバージョン

## 問題

[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicでアラートが届きます。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、マーチャントに標準のアラートセットを提供するために、Adobeで開発されました。

**<u>動け！</u>**

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、インストールガイドの [ インストールガイド/メンテナンスモードの有効化または無効化 ](/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html#enable-or-disable-maintenance-mode-1) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、インストール ガイドの [ 除外 IP アドレスのリストを管理する ](/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html#maintain-the-list-of-exempt-ip-addresses) を参照してください。

**<u>やめて！</u>**

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（データの読み込み/書き出し、メディアのフラッシュ、多数の割り当てられた商品を含むカテゴリの保存、一括更新など、Commerce管理者での主要なアクション）を実行します。
* キャッシュをクリアします。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

**これは重大なアラートなので、問題のトラブルシューティングを行う（手順 2 以降）前に手順 1 を完了することを強くお勧めします。**

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、サポートナレッジベースの [ サポートチケットの追跡 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) を参照してください。 サポートは、既にNew Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。

   * 連絡先の理由：「New Relicの重大なアラートを受信しました」を選択します。
   * アラートの説明。
   * [New Relic インシデントのリンク ](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents/). これは、[Adobe Commerceの管理アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) に含まれています。

1. サポートチケットが存在しない場合は、[one.newrelic.com](https://login.newrelic.com)/**インフラストラクチャ**/**サードパーティサービス** ページに移動して、Redis の使用メモリが増加または減少しているかどうかを確認し、Redis ダッシュボードを選択します。 安定しているか増加している場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、クラスターをアップサイズするか、`maxmemory` 限を次のレベルに上げます。
1. Redis メモリ消費量が増加した原因を特定できない場合は、最近の傾向を確認して、最近のコードのデプロイメントまたは構成の変更に関する問題（新しい顧客グループやカタログの大幅な変更など）を特定します。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. サードパーティの拡張機能の動作が正しくないことを確認します。

   * 最近インストールしたサードパーティの拡張機能と、問題が発生した時刻との相関関係を確認します。
   * Adobe Commerceのキャッシュに影響を与え、キャッシュが急速に大きくなる可能性がある拡張機能を確認します。 例えば、カスタムレイアウトブロック、キャッシュ機能の上書き、キャッシュへの大量データの保存などです。

1. 拡張機能の動作に誤りがある証拠がない場合は、[ クラウドインフラストラクチャ上のAdobe Commerceの Redis の問題を修正するための最新のパッチをインストールする ](/help/troubleshooting/miscellaneous/install-latest-patches-to-fix-magento-redis-issues.md) を参照してください。
1. 上記の手順で問題の原因を特定またはトラブルシューティングできない場合は、L2 キャッシュを有効にして、アプリと Redis 間のネットワークトラフィックを減らすことを検討してください。 L2 キャッシュの概要については、開発者向けドキュメントの [Adobe Commerce アプリケーションの L2 キャッシュ ](/docs/commerce-operations/configuration-guide/cache/level-two-cache.html) を参照してください。 クラウドインフラストラクチャの L2 キャッシュを有効にするには、次の操作を試します。

   * 2002.1.2 バージョン未満の場合は、ECE ツールをアップグレードします。
   * [REDIS\_BACKEND 変数を使用 ](/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#redis_backend) を使用し、ファイルを更新して、L2 キャッシュ `.magento.env.yaml` 設定します。

   ```yaml
   stage:
       deploy:
           REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
   ```
