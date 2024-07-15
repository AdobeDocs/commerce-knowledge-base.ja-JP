---
title: クラウドインフラストラクチャ cron ジョブでスタックしたAdobe Commerceを手動でリセット
description: クラウドインフラストラクチャー上のAdobe Commerce cron ジョブの実行が完了せず、停止し、他の cron ジョブの実行を妨げる。 この記事では、停止した cron ジョブを手動でリセットする方法を説明します。
exl-id: aec6de8e-c3a9-4a6d-8ecd-a213e77c97a1
feature: Cloud
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# クラウドインフラストラクチャ cron ジョブでスタックしたAdobe Commerceを手動でリセット

クラウドインフラストラクチャー上のAdobe Commerce cron ジョブの実行が完了せず、停止し、他の cron ジョブの実行を妨げる。 この記事では、停止した cron ジョブを手動でリセットする方法を説明します。

このコマンドは慎重に使用してください。 詳しくは、サポートナレッジベースで [cron ジョブのリセット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html) の記事を読むことをお勧めします。

## 手順

>[!INFO]
>
>[ECE-Tools v2002.0.4 から ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/release-notes/cloud-release-archive.html#v2002.0.4)SSH アクセスを介して CLI コマンドを使用して、スタックした cron ジョブを手動でリセットできます。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 次のコマンドを実行します：`./vendor/bin/ece-tools cron:unlock`

## 警告

* このコマンドは、現在実行中の cron ジョブを含め、**すべて** cron ジョブをリセットします。**例外的な場合にのみ使用**。
* インデクサーを実行している場合は、この解決策を使用しないでください。

## 詳しくは、サポートナレッジベースを参照してください。

[cron ジョブのリセット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html)
