---
title: 'クラウド上のバックアップ（スナップショット）：よくある質問'
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境をスナップショットでバックアップする際の基本事項について説明します。
exl-id: 0077db74-3e7e-4c98-b215-7f6c089f49e8
feature: Cloud, Iaas
source-git-commit: 0958a8923e27c1341f4b536812b26205685b2b81
workflow-type: tm+mt
source-wordcount: '550'
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
* 自動スナップショットが作成される **ライブ状態に関係なく** （まだ起動されていないサイト用にスナップショットも作成されます） 自動バックアップは、別のシステムに保存されているので、公開ではアクセスできません。 次のことができます [Adobe Commerce サポートチケットを送信](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) チケットに日付、時刻、タイムゾーンを指定して、特別なバックアップを要求したり、特定のバックアップからリストアしたりすること。 また、データベースのロールバックやリストアはサポートによって実行されず、スナップショットが取得されますが、データベースは自分でリストアする必要があります。
* バックアップは、 **暗号化されたAmazon Web Services Elastic Block Store （AWS EBS）スナップショット**.
* 環境スナップショットには、完全なシステム（ファイルシステムとデータベース）が含まれます。
* 自動スナップショットのリテンション時間 **が異なる** およびが続きます [スケジュール](/docs/commerce-cloud-service/user-guide/architecture/pro-architecture.html?lang=en#backup-and-disaster-recovery).

>[!NOTE]
>Cloud Console には常に以下が表示されます。 [!UICONTROL No backup] ステージング環境および実稼動環境で使用します。 バックアップを作成できるのは、統合環境からのみです。 を選択 **[!UICONTROL Backup]** 「。..」ドロップダウンメニューで、をクリックします。
>![cloud_console_backup.png](assets/cloud_console_backup.png)





### 統合（開発）環境

* あなたの [統合環境](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) 等しい **自動的にバックアップされない**&#x200B;ただし、スナップショットを作成することはできます **手動**.
* 非ライブストアの統合環境に対して、手動スナップショットを作成できます。
* 以下が含まれる場合があります。 **複数のスナップショット** 手動でトリガーされたもの
* 手動でトリガーされたスナップショットは、 **7 日間**.

**開発者向けドキュメントの関連記事：**

* [バックアップと障害回復](/docs/commerce-cloud-service/user-guide/architecture/pro-architecture.html#backup-and-disaster-recovery)
* [スナップショットの作成](/docs/commerce-cloud-service/user-guide/develop/storage/snapshots.html)

## 環境スナップショット、スタータープラン

* すべてのタイプの環境（統合、ステージング、実稼動） **自動的にバックアップされない**&#x200B;ただし、スナップショットは手動で作成できます。
* 手動スナップショットを作成できます **ライブ状態に関係なく** （まだ起動されていないサイト用にスナップショットも作成されます）
* 手動でトリガーされたスナップショットは、 **7 日間**.

## 環境スナップショットの復元

既存のスナップショットを復元するには（サポート対象の環境：統合、ステージング、スタータープランの実稼動または Pro プランの統合）、次の手順に従います [バックアップ管理：手動バックアップの復元](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots#restore-a-manual-backup) クラウドインフラストラクチャーに関するCommerceのガイドを参照してください。

## データベース（DB）のバックアップ

DB バックアップは、クラウドスナップショットの一部です。

>>
スナップショットは、環境の完全なバックアップであり、実行中のすべてのサービス（など）からのすべての永続的なデータが含まれます **mysql データベース**、Redis など）と、マウントされたボリュームに保存されているファイル。

>[!NOTE]
>
>マウントされたボリュームは、 [書き込みマウント](/docs/commerce-cloud-service/user-guide/configure/app/properties/properties.html?lang=en#mounts) とは/app ディレクトリのすべてが含まれるわけではありません。 その他のファイルの場合は、によって作成または生成されます。 [ビルドおよびデプロイメントプロセス](/docs/commerce-cloud-service/user-guide/architecture/pro-develop-deploy-workflow.html?lang=en#deployment-workflow)また、残りのファイルを Git リポジトリからチェックアウトする必要もあります。

[スナップショットとバックアップ管理](/docs/commerce-cloud-service/user-guide/develop/storage/snapshots.html) 開発者向けドキュメントを参照してください。

のみを送信 [サポートリクエスト](/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) 特定の時点からの DB が必要な場合、実稼動環境およびステージング環境からの DB スナップショット用。 （任意の環境で） DB の現在のバックアップのみが必要な場合は、ナレッジベースの記事を参照してください。 [クラウドでのデータベースダンプの生成](/help/how-to/general/create-database-dump-on-cloud.md).
