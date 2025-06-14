---
title: クラウド上のバックアップ（スナップショット）：よくある質問
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境をスナップショットでバックアップする際の基本事項について説明します。
exl-id: 0077db74-3e7e-4c98-b215-7f6c089f49e8
feature: Cloud, Iaas
source-git-commit: 3df2d07bb5765fb0ddcb4417b7c4e4ae33ef2d42
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# クラウド上のバックアップ（スナップショット）：よくある質問

この記事では、クラウドインフラストラクチャー上のAdobe Commerceのスナップショットを使用した環境のバックアップについて説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.x 上のAdobe Commerce
* アーキテクチャプラン：スターター、プロレガシー、プロ

## 環境スナップショット、プロプラン

### ステージング環境と実稼動環境

* 手動スナップショットは、Pro プランのステージング環境および実稼動環境では使用できません。
* 自動スナップショットは、サイトの **ライブ状態に関係なく** 作成されます（まだ起動されていないサイトに対してもスナップショットが作成されます）。 自動バックアップは、別のシステムに保存されているので、公開ではアクセスできません。
[Adobe Commerce サポートチケットを送信 ](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) して、特別なバックアップをリクエストしたり、チケットに日付、時刻、タイムゾーンを指定した特定のバックアップから復元したりできます。 インフラストラクチャチームがスナップショットを指定したら、最初に取得されたタイムスタンプを判断するために、スナップショットが配置されている場所から次のコマンドを実行します。

  `cat /mnt/recovery/vol-<volume_id>/snap.time`

  出力例：

  <strong>2025-01-13 08:42:17.123000+00:00</strong>


* サポートでは、オンデマンドで手動スナップショットは生成されません。 また、データベースのロールバックやリストアはサポートによって実行されず、スナップショットが取得されますが、データベースは自分でリストアする必要があります。
* 自動スナップショットは、サイトの **ライブ状態に関係なく** 作成されます（まだ起動されていないサイトに対してもスナップショットが作成されます）。 自動バックアップは別のシステムに保存され、一般にはアクセスできません。
[Adobe Commerce サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md) して、特別なバックアップをリクエストしたり、チケットに日付、時刻、タイムゾーンを指定した特定のバックアップから復元したりできます。 サポートでは、オンデマンドで手動スナップショットは生成されません。
また、データベースのロールバックやリストアはサポートによって実行されず、スナップショットが取得されますが、データベースは自分でリストアする必要があります。
* バックアップは、**暗号化されたAmazon Web Services Elastic Block Store （AWS EBS）スナップショット** を使用して作成されます。
* 環境スナップショットには、完全なシステム（ファイルシステムとデータベース）が含まれます。
* 自動スナップショットのリテンション時間 **異なる** と [ スケジュール ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/architecture/pro-architecture#backup-and-disaster-recovery) に従います。

>[!NOTE]
>
>Cloud Console は、ステージング環境と実稼動環境では常に [!UICONTROL No backup] を表示します。 バックアップを作成できるのは、統合環境からのみです。 省略記号ドロップダウンメニューの「**[!UICONTROL Backup]**」を選択します。
>
>![cloud_console_backup.png](assets/cloud_console_backup.png)

### 統合（開発）環境

* [ 統合環境 ](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) は **自動的にバックアップされていません** が、スナップショットを **手動** 作成できます。
* 非ライブストアの統合環境に対して、手動スナップショットを作成できます。
* 手動でトリガーされた **複数のスナップショット** がある場合があります。
* 手動でトリガーしたスナップショットは、**7 日間** 保存されます。

**関連記事については、開発者向けドキュメントを参照してください。**

* [ バックアップと災害復旧 ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/architecture/pro-architecture#backup-and-disaster-recovery)
* [ スナップショットの作成 ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/develop/storage/snapshots)

## 環境スナップショット、スタータープラン

* すべてのタイプの環境（統合、ステージング、実稼動） **自動的にバックアップされるわけではありません** で、スナップショットを手動で作成することもできます。
* サイトの **ライブ状態に関係なく** 手動のスナップショットを作成できます（まだ起動されていないサイト用のスナップショットも作成されます）。
* 手動でトリガーしたスナップショットは、**7 日間** 保存されます。

## 環境スナップショットの復元

Commerce既存のスナップショットを復元するには（サポート対象の環境：統合、ステージング、スタータープランの実稼動または Pro プランの統合）、Cloud Infrastructure ガイドの [ バックアップ管理：手動バックアップの復元 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/snapshots#restore-a-manual-backup) の手順に従ってください。

## データベース（DB）のバックアップ

DB バックアップは、クラウドスナップショットの一部です。

スナップショットは、環境の完全なバックアップです。このバックアップには、実行中のすべてのサービス（**MySQL データベース**、Redis など）のすべての永続的なデータと、マウントされたボリュームに保存されているファイルが含まれます。

>[!NOTE]
>
>マウントされたボリュームは [ 書き込み可能なマウント ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/configure/app/properties/properties#mounts) のみを含み/参照し、`/app` ディレクトリの一部は含みません。 その他のファイルの場合は、[ ビルドおよびデプロイメントプロセス ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/architecture/pro-develop-deploy-workflow#deployment-workflow) によって作成および生成されます。また、Git リポジトリから残りのファイルをチェックアウトする必要もあります。

開発者向けドキュメントの [ スナップショットとバックアップ管理 ](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/develop/storage/snapshots)。

特定の時点から DB が必要な場合は、実稼動環境およびステージング環境から DB スナップショットの [ サポートリクエスト ](/help/help-center-guide/help-center/magento-help-center-user-guide.md) を送信するだけです。 （任意の環境で）現在の DB のバックアップのみが必要な場合は、ナレッジベースの記事 [ クラウドでのデータベースダンプの生成 ](/help/how-to/general/create-database-dump-on-cloud.md) を参照してください。
