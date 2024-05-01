---
title: Adobe Commerce導入のトラブルシューティング
description: Adobe Commerceでのスタックしたデプロイメントと失敗したデプロイメントは、デプロイメントのトラブルシューティング ツールを使用して解決できます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。
exl-id: 5141e079-be61-44c2-8bff-c4b13cb7e07c
feature: Build, Deploy, Support
role: Developer
source-git-commit: 6177863da268f43cc30119cef6f718a04c46b3e6
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Adobe Commerce導入のトラブルシューティング

Adobe Commerceでのスタックしたデプロイメントと失敗したデプロイメントは、デプロイメントのトラブルシューティング ツールを使用して解決できます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。

## 手順 1 - サービスが実行中であることを確認 {#step-1}

+++**Adobe Commerce on cloud infrastructure service は稼働していますか？**

デプロイメントの停止 – クラウドインフラストラクチャサービス上でAdobe Commerceは稼働していますか。 チェック [Adobe Commerce Cloud](https://status.adobe.com/products/3350/).

a.はい – に進みます。 [手順 2](#step-2).\
b. NO - メンテナンスまたはグローバルな障害。 推定期間と更新を確認します。

+++

## 手順 2 – 他の環境でのデプロイメントの確認 {#step-2}

+++**既存の環境でデプロイメントをブロックしているデプロイメントが他の環境にありますか？**

進行中のアクティビティのリストを取得するには、magento-cloud CLI を使用して次のコマンドを実行します（1 つのクラウドプロジェクトにのみ追加されている場合）。

```bash
magento-cloud --state=in_progress
```

進行中のアクティビティのリストを取得するには、magento-cloud CLI を使用して次のコマンドを実行します（複数のプロジェクトに追加されている場合）。

```bash
magento-cloud -p <project-id or project-url> --state=in_progress
```

既存のデプロイメントアクティビティに関する情報を検索するには、以下を参照してください [Cloud UI に「ログのスニペット」エラーがあるかどうかをデプロイメントログで確認しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error.html)
詳しくは、次のコマンドを実行して、そのアクティビティの実行ログを取得してください。

```bash
magento-cloud activity:log <activity-id> [OPTIONAL: <-p project-id or project-url>]
```

a.はい – 既存の環境でデプロイメントがブロックされている他の環境のトラブルシューティングを行います。 次の手順に進みます。 [手順 3](#step-3).

b.いいえ – 現在の環境のトラブルシューティングを行います。 次の手順に進みます。 [手順 3](#step-3).

+++


## 手順 3 – すべてのノードで SSH を確認する {#step-3}

+++**すべてのノードで SSH に成功しますか？**

a.はい – に進みます。 [手順 4](#step-4).\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 4 – 実行中のすべてのサービスの確認 {#step-4}

+++**すべてのサービスが実行中ですか？**

a.はい – に進みます。 [手順 5](#step-5).\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 5 - ビットバケットの実行状態の確認 {#step-5}

+++**Bitbucket を使用しますか？**

a.はい – 確認 [status.bitbucket.com](https://bitbucket.status.atlassian.com/).\
b. NO – のデプロイメントログエラーを確認する [ログの作成とデプロイ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html). 次の手順に進みます。 [手順 6](#step-6).

+++

## 手順 6 - エラーコードを確認 {#step-6}

+++**エラーコードが報告されていますか？**

a.はい – に進みます。 [手順 7](#step-7).\
b.いいえ – に進みます。 [手順 8](#step-8).

+++

## 手順 7 - 403 Forbidden エラー {#step-7}

+++**403 禁断？**

a.はい – に進みます。 [手順 16](#step-16).
b.いいえ – に進みます。 [手順 9](#step-9).

+++

## 手順 8 – 実行中の cron ジョブの確認 {#step-8}

+++**cron ジョブは現在実行中ですか？** ブランチで ssh を使用してログインし、 `ps aufxx |grep cron`.

a.はい – 該当するブランチ（プライマリなど）で ssh でログインします。 Cron ジョブを強制終了してロックを解除します。 これにより、cron ジョブが強制終了し、ステータスがリセットされます。 実行 `php vendor/bin/ece-tools cron:kill` その後 `php vendor/bin/ece-tools cron:unlock`. ある環境を別の環境に結合する処理を行っている場合は、両方の環境で cron が動作しているかどうかを確認します。\
b.いいえ – に進みます。 [手順 17](#step-17).

+++

## 手順 9 - リモートクラスターにデプロイ可能なアプリケーションのエラー {#step-9}

+++**リモートクラスターにアプリケーションをアップロードできないというエラーが発生しましたか？**

a.はい – に進みます。 [手順 10](#step-10).\
b.いいえ – に進みます。 [手順 11](#step-11).

+++

## 手順 10 – 十分なストレージの確認 {#step-10}

+++**使用可能なストレージは問題ない？**

a.はい – 次に進みます。 [手順 11](#step-11).\
b.いいえ – レビュー [ディスク容量の管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html).

+++

## 手順 11 - ディスク容量の確認 {#step-11}

+++**_ファイルに警告を書き込めませんでした&#x200B;_?**

a.はい – お願いします [.magento.app.yaml のディスク値を増やす](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html#application-disk-space) を実行して再デプロイします。 これが機能しない場合、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b.いいえ – 続行します。 [手順 12](#step-12).

+++

## 手順 12 – 環境の再デプロイメントに失敗しましたエラー {#step-12}

+++**環境の再デプロイメントに失敗しましたエラーですか？**

a.はい – 次に進みます。 [手順 13](#step-13).\
b.いいえ – 続行します。 [手順 8](#step-8).

+++

## 手順 13 - Elasticsearchのアップグレードに失敗したかどうかを確認する {#step-13}

+++**アップグレードまたはデプロイするElasticsearchですか？**

a.はい – Elasticsearchがアップグレード手順に失敗しました。 こちらを参照してください [Elasticsearchソフトウェアの互換性](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-upgrade.html). それでもElasticsearchのアップグレードが機能しない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket). **注意**: クラウドインフラストラクチャー上のAdobe Commerceの場合、インフラストラクチャチームに 48 営業時間通知しなければ、サービスアップグレードを実稼動環境にプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要があるのは、48 時間前までということになります。 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 必要なサービスのアップグレードの詳細を説明し、アップグレードプロセスを開始する時刻を指定します。\
b.いいえ – に進みます。 [手順 14](#step-14).

+++

## 手順 14 - スペース制限を確認 {#step-14}

+++**ファイル・システムの inode またはスペースが不足している場合**

a.はい – を参照 [ディスク容量の管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html#application-disk-space).\
b.いいえ – に進みます。 [手順 15](#step-15).

+++

## 手順 15 - Elasticsearchバージョンのエラー {#step-15}

+++**Elasticseach バージョンに関するエラー**

a.はい – に進みます。 [手順 16](#step-16).\
b.いいえ – に進みます。 [手順 21](#step-21).

+++

## 手順 16 - Composer 設定の確認 {#step-16}

+++**コンポーザーの構成は正しいですか？**

a.はい – に進みます。 [手順 10](#step-10).\
b.いいえ – レビュー [Composer に関するトラブルシューティングの web ページ](https://getcomposer.org/doc/articles/troubleshooting.md).

+++

## 手順 17 – 長時間実行されているプロセスの確認 {#step-17}

+++**長時間実行されているプロセスは？**

a.はい。長時間実行されているプロセスを特定し、プロセスを強制終了します。
1. ターミナルで次のコマンドを実行します。 `ps aufx`.
1. 長時間実行されているプロセスの PID を見つけます。
1. を使用してプロセスを終了する `kill -9 <PID>`.

再び発生する展開を監視します。

b.いいえ – に進みます。 [手順 18](#step-18).

+++

## 手順 18 - ポストフックの失敗を確認する {#step-18}

+++**フック後のエラー/ハング？**

a.はい – データベース： [空きディスク容量](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html#allocate-disk-space)、破損、不完全/破損したテーブル。\
b.いいえ – に進みます。 [手順 19](#step-19).

+++

## 手順 19 - サードパーティの拡張機能でデプロイメントがブロックされているかどうかを確認する {#step-19}

+++**サードパーティの拡張機能を使用している場合は、**

a.はい – 試す [サードパーティの拡張機能の無効化](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html) デプロイメントを実行します（問題の原因であるかどうかを確認するため）（特にエラーで拡張機能名がある場合）。\
b.いいえ – に進みます。 [手順 20](#step-20).

+++

## 手順 20 – 処理に時間のかかるクエリの確認 {#step-20}

+++**長時間実行されているクエリは？**

[低速のクエリログと MySQL 表示プロセスリストを確認](/help/troubleshooting/database/checking-slow-queries-and-processes-mysql.md).

a.はい – 長時間実行中のクエリを強制終了します。 レビュー [MySQL Kill 構文。](https://dev.mysql.com/doc/refman/8.0/en/kill.html)\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 21 - Elasticsearchのバージョンのダウングレード {#step-21}

+++**Elasticsearchのバージョンをダウングレードしますか？**

a.はい – 設定では実行できません。 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

[手順 1 に戻る](#step-1)
