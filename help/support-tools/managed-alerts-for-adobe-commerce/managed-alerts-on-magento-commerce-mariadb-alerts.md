---
title: 「Adobe Commerceの管理アラート：MariaDB アラート」
description: 「この記事では、New RelicでAdobe Commerceの MariaDB アラートを受信した場合のトラブルシューティング手順を説明します。 MariaDB アラートは、高いクエリ負荷と過剰なデータ操作言語（DML）クエリを監視します。 どちらも、ユーザーエクスペリエンスの低下やダウンタイムにつながる可能性があります。 次の 4 種類のアラートを受信できます。'
exl-id: 707e20e0-faba-4bcd-884c-b54568787442
feature: Cache, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：MariaDB アラート

この記事では、New RelicでAdobe Commerceの MariaDB アラートを受信した場合のトラブルシューティング手順を説明します。 MariaDB アラートは、高いクエリ負荷と過剰なデータ操作言語（DML）クエリを監視します。 どちらも、ユーザーエクスペリエンスの低下やダウンタイムにつながる可能性があります。 次の 4 種類のアラートを受信できます。

* DML 問合せの警告
* DML 問合せクリティカル

## **影響を受ける製品とバージョン**

Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ

## 問題

[Adobe Commerceの管理アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicで管理アラートを受け取ります。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

**動け！**

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、「[ 除外 IP アドレスのリストの管理 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode#instgde-cli-maint-exempt)」を参照してください。
* サイトパフォーマンスに影響が出ている場合は、読み込みなどのスクリプトを終了し、アラートの原因を特定してください。

**やめて！**

* MariaDB に追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データのインポート/エクスポートなど）を実行します。
* キャッシュをクリアします。

## 解決策

**DML 問合せ（UPDATE、INSERT およびDELETEを使用してデータベースを変更する問合せ）**

DML 問合せクリティカル・アラートを受け取った場合は、手順 1 から開始します。 DML クエリの警告アラートを受け取った場合は、手順 2 から開始します。

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、ナレッジベース [ サポートチケットの追跡 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) を参照してください。 サポートは、New Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。
1. 連絡先の理由：「New Relic MariaDB アラートを受信しました」を選択します。
1. アラートの説明。
1. [New Relic インシデントのリンク ](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents)。 これは、[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) に含まれています。
1. 問題の原因を特定するには、DML 問合せを特定します。
1. New Relic[APM UI ページ/モニタリング/データベースページ ](https://docs.newrelic.com/docs/apm/apm-ui-pages/monitoring/databases-page-view-operations-throughput-response-time) の手順を使用して、データベース操作を確認します。
1. コール数、オペレーションの順に並べ替えます。 INSERT、DELETE、および UPDATE 操作を確認します。
1. 高い AVG を探します。
1. クリックスルーしてデータベース操作呼び出し元を検索します。 これにより、そのクエリを使用しているトランザクションが時間別に識別されます。
1. コードの最適化または運用の最適化を探します。
1. コードの最適化：一括挿入/更新、インデックス使用の最小化、コードのスロットルなどを使用してクエリを最適化する場合を想定しています。
1. 運用の最適化：リソースを大量に消費するデータ変更の負荷を軽減し、トラフィック時間を短縮します。
1. その他の最適化：ECE-Tools の最新バージョンを使用していることを確認してください。 手順については、開発者向けドキュメントの [Cloud for Adobe Commerce/ece-tools バージョンの更新 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/update-package) を参照してください。

## 関連資料

* その他の一般的な MariaDB の問題を調査するには、[ クラウドインフラストラクチャー上のAdobe Commerceで最も一般的なデータベースの問題 ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html) を参照してください。
* データベースのベストプラクティスについて詳しくは、[ クラウドインフラストラクチャー上のAdobe Commerceに関するデータベースのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud.html) を参照してください。
