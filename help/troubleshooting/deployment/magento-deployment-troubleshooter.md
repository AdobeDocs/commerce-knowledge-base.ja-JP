---
title: Adobe Commerce導入のトラブルシューティング
description: Adobe Commerceでのスタックしたデプロイメントと失敗したデプロイメントは、デプロイメントのトラブルシューティング ツールを使用して解決できます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。
exl-id: 5141e079-be61-44c2-8bff-c4b13cb7e07c
feature: Build, Deploy, Support
role: Developer
source-git-commit: 4704446d043e3175b5af27c068908e58bfb7a9ff
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Adobe Commerce導入のトラブルシューティング

Adobe Commerceでのスタックしたデプロイメントと失敗したデプロイメントは、デプロイメントのトラブルシューティング ツールを使用して解決できます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。

## 手順 1 - サービスが実行中であることを確認 {#step-1}

+++**クラウドインフラストラクチャサービス上のAdobe Commerceは稼働していますか？**

デプロイメントの停止 – クラウドインフラストラクチャサービス上でAdobe Commerceは稼働していますか。 「[Adobe Commerce Cloud](https://status.adobe.com/products/3350/)」をオンにします。

a.はい – [ 手順 2](#step-2) に進みます。\
b. NO - メンテナンスまたはグローバルな障害。 推定期間と更新を確認します。

+++

## 手順 2 – 他の環境でのデプロイメントの確認 {#step-2}

+++**既存の環境のデプロイメントをブロックしているデプロイメントが他の環境にありますか？**

進行中のアクティビティのリストを取得するには、magento-cloud CLI を使用して次のコマンドを実行します（1 つのクラウドプロジェクトにのみ追加されている場合）。 **メモ**：最新バージョンの magento-cloud CLI を使用していることを確認してください。 手順については、Cloud Infrastructure 上のCommerce ガイドの [CLI の更新 ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) を参照してください。

```bash
magento-cloud --state=in_progress
```

進行中のアクティビティのリストを取得するには、magento-cloud CLI を使用して次のコマンドを実行します（複数のプロジェクトに追加されている場合）。

```bash
magento-cloud -p <project-id or project-url> --state=in_progress
```

既存のデプロイメントアクティビティに関する情報を見つけるには（[Cloud UI で「ログがスニップされた」エラーがある場合のデプロイメントログの確認」を参照 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error)
詳しくは、次のコマンドを実行して、そのアクティビティの実行ログを取得してください。

```bash
magento-cloud activity:log <activity-id> [OPTIONAL: <-p project-id or project-url>]
```

a.はい – 既存の環境でデプロイメントがブロックされている他の環境のトラブルシューティングを行います。 [ 手順 3](#step-3) に進みます。

b.いいえ – 現在の環境のトラブルシューティングを行います。 [ 手順 3](#step-3) に進みます。

+++


## 手順 3 – すべてのノードで SSH を確認する {#step-3}

+++**すべてのノードで SSH に成功しますか？**

a.はい – [ 手順 4](#step-4) に進みます。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

## 手順 4 – 実行中のすべてのサービスの確認 {#step-4}

+++**すべてのサービスが実行中ですか？**

a.はい – [ 手順 5](#step-5) に進みます。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

## 手順 5 - ビットバケットの実行状態の確認 {#step-5}

+++**Bitbucket の使用**

a.はい – [status.bitbucket.com](https://bitbucket.status.atlassian.com/) をチェックします。\
b.いいえ – [ ビルドおよびデプロイログ ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/log-locations) でデプロイメントログエラーを確認します。 [ 手順 6](#step-6) に進みます。

+++

## 手順 6 - エラーコードを確認 {#step-6}

+++**エラーコードが報告されていますか？**

a.はい – [ 手順 7](#step-7) に進みます。\
b.いいえ – [ 手順 8](#step-8) に進みます。

+++

## 手順 7 - 403 Forbidden エラー {#step-7}

+++**403 Forbidden?**

a.はい – [ 手順 16](#step-16) に進みます。
b.いいえ – [ 手順 9](#step-9) に進みます。

+++

## 手順 8 – 実行中の cron ジョブの確認 {#step-8}

+++**cron ジョブは現在実行中ですか？** 分岐に ssh でログインし、`ps aufxx |grep cron` を実行します。

a.はい – 該当するブランチ（プライマリなど）で ssh でログインします。 Cron ジョブを強制終了してロックを解除します。 これにより、cron ジョブが強制終了し、ステータスがリセットされます。 `php vendor/bin/ece-tools cron:kill` を実行し、次に `php vendor/bin/ece-tools cron:unlock` を実行します。 ある環境を別の環境に結合する処理を行っている場合は、両方の環境で cron が動作しているかどうかを確認します。\
b.いいえ – [ 手順 17](#step-17) に進みます。

+++

## 手順 9 - リモートクラスターにデプロイ可能なアプリケーションのエラー {#step-9}

+++**リモートクラスターにアプリケーションをアップロードできないというエラーが発生しましたか？**

a.はい – [ 手順 10](#step-10) に進みます。\
b.いいえ – [ 手順 11](#step-11) に進みます。

+++

## 手順 10 – 十分なストレージの確認 {#step-10}

+++**使用可能なストレージは問題ありませんか？**

a.はい – [ 手順 11](#step-11) に進みます。\
b. NO - レビュー [ ディスク容量の管理 ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/storage/manage-disk-space)。

+++

## 手順 11 - ディスク容量の確認 {#step-11}

+++**_ファイルに警告を書き込めませんでした _?**

a.はい。[.magento.app.yaml のディスク値を増やして ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html#application-disk-space) 再デプロイしてください。 それでもうまくいかない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。\
b.いいえ – [ 手順 12](#step-12) に進みます。

+++

## 手順 12 – 環境の再デプロイメントに失敗しましたエラー {#step-12}

+++**環境の再デプロイメントに失敗しましたエラー？**

a.はい – [ 手順 13](#step-13) に進みます。\
b.いいえ – [ 手順 8](#step-8) に進みます。

+++

## 手順 13 - Elasticsearchのアップグレードに失敗したかどうかを確認する {#step-13}

+++**Elasticsearchをアップグレードまたはデプロイしますか？**

a.はい – Elasticsearchのアップグレード手順に失敗しました。 [Elasticsearch ソフトウェア互換性 ](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-upgrade.html) を参照してください。 それでもElasticsearchのアップグレードが機能しない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。 **注意**：クラウドインフラストラクチャー上のAdobe Commerceでは、インフラストラクチャチームに 48 営業時間通知しないと、実稼動環境にサービスアップグレードをプッシュできないことに注意してください。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある場合は、48 時間前に [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、必要なサービスアップグレードの詳細を説明し、アップグレードプロセスを開始する時刻を指定します。\
b.いいえ – [ 手順 14](#step-14) に進みます。

+++

## 手順 14 - スペース制限を確認 {#step-14}

+++**ファイル・システムの inode またはスペースが不足している場合**

a.はい。[ ディスク容量の管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html#application-disk-space) を参照してください。\
b.いいえ – [ 手順 15](#step-15) に進みます。

+++

## 手順 15 - Elasticsearchのバージョンエラー {#step-15}

+++**Elasticseach バージョンに関するエラー**

a.はい – [ 手順 16](#step-16) に進みます。\
b.いいえ – [ 手順 21](#step-21) に進みます。

+++

## 手順 16 - Composer 設定の確認 {#step-16}

+++**Composer の設定は正しいですか？**

a.はい – [ 手順 10](#step-10) に進みます。\
b.いいえ – [Composer トラブルシューティング Web ページ ](https://getcomposer.org/doc/articles/troubleshooting.md) を確認します。

+++

## 手順 17 – 長時間実行されているプロセスの確認 {#step-17}

+++**長時間実行されているプロセス**

a.はい。長時間実行されているプロセスを特定し、プロセスを強制終了します。
1. ターミナルで次のコマンドを実行します：`ps aufx`。
1. 長時間実行されているプロセスの PID を見つけます。
1. `kill -9 <PID>` を使用してプロセスを終了します。

再び発生する展開を監視します。

b.いいえ – [ 手順 18](#step-18) に進みます。

+++

## 手順 18 - ポストフックの失敗を確認する {#step-18}

+++**ポストフックの失敗/ハングアップ？**

a.はい – データベース：[ 空きディスク領域 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space.html#allocate-disk-space)、破損、不完全/破損したテーブル。\
b.いいえ – [ 手順 19](#step-19) に進みます。

+++

## 手順 19 - サードパーティの拡張機能でデプロイメントがブロックされているかどうかを確認する {#step-19}

+++**サードパーティの拡張機能を使用しますか？**

回答：はい [ サードパーティの拡張機能を無効にする ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions) を試して、特にエラーに拡張機能名がある場合は、デプロイメントを実行します（問題の原因がサードパーティの拡張機能であるかどうかを確認します）。\
b.いいえ – [ 手順 20](#step-20) に進みます。

+++

## 手順 20 – 処理に時間のかかるクエリの確認 {#step-20}

+++**長時間実行中のクエリ**

[ 低速のクエリログと MySQL show processlist を確認してください ](/help/troubleshooting/database/checking-slow-queries-and-processes-mysql.md)。

a.はい – 長時間実行中のクエリを強制終了します。 [MySQL Kill 構文。](https://dev.mysql.com/doc/refman/8.0/en/kill.html) を確認します。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

## 手順 21 - Elasticsearchのバージョンのダウングレード {#step-21}

+++**Elasticsearchのバージョンをダウングレードしますか？**

a.はい – 設定では実行できません。 [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

[手順 1 に戻る](#step-1)
