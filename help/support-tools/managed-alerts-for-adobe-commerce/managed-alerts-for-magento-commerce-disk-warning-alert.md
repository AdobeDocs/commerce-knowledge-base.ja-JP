---
title: 「Adobe Commerceの管理アラート：disk warning アラート」
description: この記事では、New RelicでAdobe Commerceの警告ディスクアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 07b34db1-11ec-4cf2-ae47-cfc067f91383
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Managed alerts for Adobe Commerce:disk warning アラート

この記事では、New RelicでAdobe Commerceの警告ディスクアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![disk warning アラート ](assets/disk-warning-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、Pro プランアーキテクチャ。

## 問題

[Adobe Commerceの Managed アラート ](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) にサインアップし、1 つ以上のアラートしきい値を超えた場合、New Relicでアラートが届きます。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

<u> **動け！**</u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、開発者向けドキュメントの [ インストールガイド/メンテナンスモードの有効化または無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、開発者向けドキュメントの [ 免除 IP アドレスのリストを管理する ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode#instgde-cli-maint-exempt) を参照してください。

<u> **やめて！**</u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。 アラートの原因を調査して解決する前に「回避」アクションのいずれかを行った場合、（まだサイトの停止が発生していない場合は）サイトが応答しなくなる可能性があります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

1. New Relicでは、ディスクの使用率を最も高く確認します。 手順については、New Relicの「ストレージ」タブを参照してください [Infrastructure monitoring Hosts ページ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/)。
   * New Relicでディスクの使用量がゆっくり増加する場合は、次のオプションを試してください。
   * ディスク領域の割り当てを調整してディスク領域を最適化しています。 手順については、開発者向けドキュメントの [ ディスク容量の管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html) を参照してください。 また、より多くのディスク容量をリクエストする必要が生じる場合もあります（Adobeアカウントチームにお問い合わせください）。
   * MySQL のディスク領域をクリアします。 手順については、[MySQL のディスク容量が少ない ](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) を参照してください。
   * New Relicでディスク使用量が急激に増加している場合は、ディレクトリ内のファイルが急激に増加している原因となっている可能性があります。 次のチェックを実行します。
1. CLI/ターミナルで次のコマンドを実行して、ディスクの空き領域全体を確認し、問題を特定します。`df -h`
1. ディスク使用量が予想外に大きく、増加しているディレクトリを特定したら、影響を受けるファイルシステムを確認する必要があります。 次の例は、ファイルディレクトリ `pub/media/` を確認する方法を示しています。 これは、Adobe Commerceがログや大きなメディアファイルの保存に使用するディレクトリです。 ただし、予期しないディスク使用量を示すディレクトリに対して、次のコマンドを実行する必要があります：`du -sch ~/pub/media/*`。

端末からの出力で、ディスク使用量が急激に増加しているこれらのディレクトリの 1 つにファイルが表示されていて、そのファイルの内容が不要であることがわかっている場合は、ファイルを削除することを検討してください。 この操作に不安がある場合は、[Adobe Commerce サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。
