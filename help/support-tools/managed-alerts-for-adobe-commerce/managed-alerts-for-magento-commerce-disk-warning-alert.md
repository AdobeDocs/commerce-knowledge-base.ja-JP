---
title: 「Adobe Commerceの管理アラート：disk warning アラート」
description: この記事では、New RelicでAdobe Commerceの警告ディスクアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。
exl-id: 07b34db1-11ec-4cf2-ae47-cfc067f91383
feature: Cache, Marketing Tools, Observability, Support, Tools and External Services
role: Admin
source-git-commit: d7dcb23eee8793b6b97717827feb88c09994bd8b
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Managed alerts for Adobe Commerce:disk warning アラート

この記事では、New RelicでAdobe Commerceの警告ディスクアラートが表示された場合のトラブルシューティング手順を説明します。 この問題を修正するには、直ちに対処する必要があります。 選択したアラート通知チャネルに応じて、アラートは次のようになります。

![disk warning アラート](assets/disk-warning-magento-managed.png){width="500"}

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、Pro プランアーキテクチャ。

## 問題

に新規登録した場合は、New Relicでアラートが届きます [Adobe Commerceの管理アラート](/help/support-tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce.md) 1 つ以上のアラートしきい値を超えています。 これらのアラートは、サポートとエンジニアリングのインサイトを使用して、お客様に標準セットを提供するために、Adobeが開発しました。

<u> **動け！** </u>

* このアラートがクリアされるまで、スケジュールされている展開を中止します。
* サイトが応答しない、または完全に応答しなくなった場合は、すぐにサイトをメンテナンスモードにします。 手順については、を参照してください。 [インストールガイド/メンテナンスモードの有効化または無効化](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten) 開発者向けドキュメントを参照してください。 トラブルシューティングのためにサイトに引き続きアクセスできるように、IP を除外 IP アドレスリストに追加してください。 手順については、次を参照してください [除外 IP アドレスの一覧を管理します](https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands-maint.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=mainten#instgde-cli-maint-exempt) 開発者向けドキュメントを参照してください。

<u> **止めて！** </u>

* 追加のマーケティングキャンペーンを開始すると、サイトに追加のページビューが表示される場合があります。
* CPU やディスクに追加の負荷がかかる可能性のあるインデクサーや追加のクローンを実行します。
* 主要な管理タスク（Commerce管理者、データの読み込み/書き出し）を実行します。
* キャッシュをクリアします。 アラートの原因を調査して解決する前に「回避」アクションのいずれかを行った場合、（まだサイトの停止が発生していない場合は）サイトが応答しなくなる可能性があります。

## 解決策

原因の特定とトラブルシューティングを行うには、次の手順に従います。

1. New Relicでは、ディスクの使用率を最も高く確認します。 手順については、New Relicの「ストレージ」タブを参照してください。 [「インフラストラクチャ監視ホスト」ページ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/):
   * New Relicでディスクの使用量がゆっくり増加する場合は、次のオプションを試してください。
   * ディスク領域の割り当てを調整してディスク領域を最適化しています。 手順については、次を参照してください [ディスク容量の管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html) 開発者向けドキュメントを参照してください。 また、より多くのディスク容量をリクエストする必要が生じる場合もあります（Adobeアカウントチームにお問い合わせください）。
   * MySQL のディスク領域をクリアします。 こちらを参照してください [MySQL のディスク容量が少ない](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) （手順）。
   * New Relicでディスク使用量が急激に増加している場合は、ディレクトリ内のファイルが急激に増加している原因となっている可能性があります。 次のチェックを実行します。
1. CLI/ターミナルで次のコマンドを実行して、ディスクの空き領域全体を調べ、問題を特定します。 `df -h`
1. ディスク使用量が予想外に大きく、増加しているディレクトリを特定したら、影響を受けるファイルシステムを確認する必要があります。 次の例は、ファイルディレクトリを確認する方法を示しています `pub/media/`. これは、Adobe Commerceがログや大きなメディアファイルの保存に使用するディレクトリです。 ただし、予期しないディスク使用量を示すディレクトリに対しては、次のコマンドを実行する必要があります。 `du -sch ~/pub/media/*`.

端末からの出力で、ディスク使用量が急激に増加しているこれらのディレクトリの 1 つにファイルが表示されていて、そのファイルの内容が不要であることがわかっている場合は、ファイルを削除することを検討してください。 このアクションに不安がある場合は、 [Adobe Commerce サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).
