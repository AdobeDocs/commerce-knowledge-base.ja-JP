---
title: クラウドインフラストラクチャのcron ジョブで停止しているAdobe Commerceを手動でリセットする
description: Adobe Commerce on cloud infrastructure cron ジョブが実行を完了せず、停止し、他のcron ジョブが実行されるのを防ぎます。 この記事では、スタックしたcron ジョブを手動でリセットする方法について説明します。
exl-id: aec6de8e-c3a9-4a6d-8ecd-a213e77c97a1
feature: Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%
---
# クラウドインフラストラクチャのcron ジョブで停止しているAdobe Commerceを手動でリセットする

Adobe Commerce on cloud infrastructure cron ジョブが実行を完了せず、停止し、他のcron ジョブが実行されるのを防ぎます。 この記事では、スタックしたcron ジョブを手動でリセットする方法について説明します。

このコマンドは慎重に使用してください。 詳しくは、サポートナレッジベースの「[Cron ジョブのリセット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html)」記事を参照することをお勧めします。

## 手順

>[!INFO]
>
>[ECE-Tools v2002.0.4](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/release-notes/cloud-release-archive.html#v2002.0.4)から、SSH アクセスを介してCLI コマンドを使用して、スタックしたcron ジョブを手動でリセットできます。

1. [環境へのSSH](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 次のコマンドを実行します：`./vendor/bin/ece-tools cron:unlock`

## 警告

* コマンドは、現在実行中のジョブを含め、**すべての** cron ジョブをリセットします。例外として&#x200B;**使用できるのは**&#x200B;だけです。
* インデクサーの実行中は、このソリューションを使用しないでください。

## この情報は、サポートナレッジベースでご確認ください：

[cron ジョブのリセット](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html)
