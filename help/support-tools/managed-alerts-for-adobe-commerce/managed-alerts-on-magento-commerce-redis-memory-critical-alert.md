---
title: 「Adobe Commerceの管理アラート：Redis メモリクリティカルアラート」
description: この記事では、New RelicのAdobe Commerceで Redis メモリクリティカルアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を解決するには、早急な対応が必要です。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 28e1d879-d7ca-4439-8e81-52a1fbf3ecb0
feature: Cache, Categories, Observability, Services, Support, Tools and External Services, Variables
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
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

に新規登録した場合は、New Relicでアラートが届きます [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) 1 つ以上のアラートしきい値を超えています。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、マーチャントに標準のアラートセットを提供するために、Adobeで開発されました。

**<u>動け！</u>**

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、を参照してください。 [インストールガイド/メンテナンスモードの有効化または無効化](/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html#enable-or-disable-maintenance-mode-1) インストールガイドをご覧ください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、次を参照してください [除外 IP アドレスの一覧を管理します](/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html#maintain-the-list-of-exempt-ip-addresses) インストールガイドをご覧ください。

**<u>止めて！</u>**

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（データの読み込み/書き出し、メディアのフラッシュ、多数の割り当てられた商品を含むカテゴリの保存、一括更新など、Commerce管理者での主要なアクション）を実行します。
* キャッシュをクリアします。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

**これは重大なアラートなので、問題のトラブルシューティング（手順 2 以降）を行う前に手順 1 を完了することを強くお勧めします。**

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、次を参照してください [サポートチケットのトラッキング](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) サポートナレッジベースで。 サポートは、既にNew Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。

   * 連絡先の理由：「New Relicの重大なアラートを受信しました」を選択します。
   * アラートの説明。
   * [New Relic インシデント リンク](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents/). これはに含まれています [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md).

1. サポートチケットが存在しない場合は、に移動して、Redis Used Memory が増加しているか減少しているかを確認します。 [one.newrelic.com](https://login.newrelic.com) > **インフラストラクチャ** > **サードパーティのサービス** ページで、Redis ダッシュボードを選択します。 安定しているか増加している場合、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) クラスタをアップサイズするには、または `maxmemory` 次のレベルに制限します。
1. Redis メモリ消費量が増加した原因を特定できない場合は、最近の傾向を確認して、最近のコードのデプロイメントまたは構成の変更に関する問題（新しい顧客グループやカタログの大幅な変更など）を特定します。 コードのデプロイメントまたは変更における相関関係について、過去 7 日間のアクティビティを確認することをお勧めします。
1. サードパーティの拡張機能の動作が正しくないことを確認します。

   * 最近インストールしたサードパーティの拡張機能と、問題が発生した時刻との相関関係を確認します。
   * Adobe Commerceのキャッシュに影響を与え、キャッシュが急速に大きくなる可能性がある拡張機能を確認します。 例えば、カスタムレイアウトブロック、キャッシュ機能の上書き、キャッシュへの大量データの保存などです。

1. 動作が誤っている証拠がない場合、 [クラウドインフラストラクチャー上のAdobe Commerceの Redis の問題を修正するための最新のパッチをインストールします。](/help/troubleshooting/miscellaneous/install-latest-patches-to-fix-magento-redis-issues.md).
1. 上記の手順で問題の原因を特定またはトラブルシューティングできない場合は、L2 キャッシュを有効にして、アプリと Redis 間のネットワークトラフィックを減らすことを検討してください。 L2 キャッシュの一般的な情報については、次を参照してください [Adobe Commerce アプリケーションでの L2 キャッシュ](/docs/commerce-operations/configuration-guide/cache/level-two-cache.html) 開発者向けドキュメントを参照してください。 クラウドインフラストラクチャの L2 キャッシュを有効にするには、次の操作を試します。

   * 2002.1.2 バージョン未満の場合は、ECE ツールをアップグレードします。
   * を使用した L2 キャッシュの設定 [REDIS\_BACKEND 変数の使用](/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#redis_backend) と更新 `.magento.env.yaml` ファイル：

   ```yaml
   stage:
       deploy:
           REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
   ```
