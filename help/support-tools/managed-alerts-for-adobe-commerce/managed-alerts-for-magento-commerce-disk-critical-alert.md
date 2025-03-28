---
title: 「Adobe Commerceの管理アラート：ディスク障害アラート」
description: この記事では、New RelicでAdobe Commerceの重大なディスクアラートが発生した場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 03e5694b-7689-4fbf-8781-636fa46ca0d3
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Adobe Commerceの管理アラート：disk critical アラート

この記事では、New RelicでAdobe Commerceの重大なディスクアラートが発生した場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![disk critical アラート ](assets/disk-critical-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

Adobe Commerce クラウドインフラストラクチャー on Pro プランアーキテクチャ

## 問題

[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicでアラートが届きます。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

<u> **動け！**</u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、[ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、「[ 除外 IP アドレスのリストの管理 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode#instgde-cli-maint-exempt)」を参照してください。

**やめて！**

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データのインポート/エクスポートなど）を実行します。
* キャッシュをクリアします。

アラートの原因を調査して解決する前に「回避」アクションのいずれかを行った場合、（まだサイトの停止が発生していない場合は）サイトが応答しなくなる可能性があります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

>[!WARNING]
>
>これは重大なアラートなので、問題のトラブルシューティング（手順 2 以降）を行う前に、**手順 1** を完了することを強くお勧めします。

1. Adobe Commerce サポートチケットが存在するかどうかを確認します。 手順については、サポートナレッジベースの [ サポートチケットの追跡 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#track-tickets) を参照してください。 サポートは、New Relicしきい値アラートを受け取り、チケットを作成して、問題の処理を開始した可能性があります。 チケットが存在しない場合は、作成します。 チケットには、次の情報が含まれている必要があります。
   * 連絡先の理由：「New Relicの重大なアラートを受信しました」を選択します。
   * アラートの説明。
   * [New Relic インシデントのリンク ](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-incidents/view-violation-event-details-incidents)。 これは、[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) に含まれています。
1. New Relicでは、ディスクの使用率を最も高く確認します。 手順については、New Relicの「ストレージ」タブを参照してください [Infrastructure monitoring Hosts ページ：](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#storage)
   * New Relicでディスクの使用量がゆっくり増加する場合は、次のオプションを試してください。
   * ディスク領域の割り当てを調整してディスク領域を最適化しています。 手順については、開発者向けドキュメントの [ ディスク容量の管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html) を参照してください。 また、より多くのディスク容量をリクエストする必要が生じる場合もあります（Adobeアカウントチームにお問い合わせください）。
   * MySQL のディスク領域をクリアします。 手順については、サポートナレッジベースの [MySQL のディスク容量が少ない ](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) を参照してください。
   * New Relicでディスク使用量が急激に増加している場合は、ディレクトリ内のファイルが急激に増加している原因となっている可能性があります。 次のチェックを実行します。
1. CLI/ターミナルで次のコマンドを実行して、ディスクの空き領域全体を確認し、問題を特定します。`df -h`
1. ディスク使用量が予想外に大きく、増加しているディレクトリを特定したら、影響を受けるファイルシステムを確認する必要があります。 次の例は、ファイルディレクトリ `pub/media/` を確認する方法を示しています。 これは、Commerceがログや大きなメディアファイルの保存に使用するディレクトリです。 ただし、予期しないディスク使用量を示すディレクトリに対して、次のコマンドを実行する必要があります：`du -sch ~/pub/media/*`

端末からの出力で、ディスク使用量が急激に増加しているこれらのディレクトリの 1 つにファイルが表示されていて、そのファイルの内容が不要であることがわかっている場合は、ファイルを削除することを検討してください。 この操作に不安がある場合は、[Adobe Commerce サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。
