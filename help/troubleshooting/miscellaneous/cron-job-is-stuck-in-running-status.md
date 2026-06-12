---
title: '[!DNL Cron]件のジョブが**実行中** ステータスで停止しています'
description: この記事では、Adobe Commerce [!DNL cron]  ジョブが実行を終了せず、「実行中」ステータスで保持され、他 [!DNL cron]  ジョブが実行されない場合の解決策を説明します。 これは、ネットワークの問題、アプリケーションのクラッシュ、再デプロイメントの問題など、さまざまな理由で発生する可能性があります。
exl-id: 11e01a2b-2fcf-48c2-871c-08f29cd76250
feature: Configuration
role: Developer
source-git-commit: 40766238a7ea748bff86decf75cddec28fe63bb9
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Cron]件のジョブが「実行中」ステータスで停止しています

この記事では、Adobe Commerce [!DNL cron] ジョブが実行を終了せず、「実行中」ステータスで保持され、他の[!DNL cron] ジョブが実行されない場合の解決策について説明します。 これは、ネットワークの問題、アプリケーションのクラッシュ、再デプロイメントの問題など、さまざまな理由で発生する可能性があります。

## 影響を受ける製品とバージョン

Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

## 症状 {#symptom}

リセットが必要な[!DNL cron] ジョブの症状は次のとおりです。

* 大量のジョブが`cron_schedule` キューに表示されます
* サイトパフォーマンスが低下し始める
* ジョブがスケジュールで実行できない

## 解決策 {#solutions}

### すべての[!DNL cron] ジョブを一度に停止するソリューション {#solution-stop-all-crons-at-once}

>[!WARNING]
>
>このコマンドを`--job-code` オプションを使用せずに実行すると、現在実行中のジョブを含む&#x200B;*すべての* [!DNL cron] ジョブがリセットされるので、すべての[!DNL cron] ジョブをリセットする必要があることを確認した後など、例外的な場合にのみ使用することをお勧めします。 再デプロイメントでは、デフォルトでこのコマンドが実行され、[!DNL cron]個のジョブがリセットされるので、環境のバックアップ後に適切に回復します。 インデクサーの実行中は、このソリューションを使用しないでください。

この問題を解決するには、`cron:unlock` コマンドを使用して[!DNL cron] ジョブをリセットする必要があります。 このコマンドは、データベース内の[!DNL cron] ジョブのステータスを変更し、ジョブを強制的に終了して、他のスケジュールされたジョブを続行できるようにします。

1. ターミナルを開き、[SSH キー](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections)を使用して、影響を受ける環境に接続します。
1. MySQL データベースの資格情報を取得：`echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp`
1. `mysql`を使用してデータベースに接続：`mysql -hdatabase.internal -uuser -ppassword main`
1. `main` データベースを選択：`use main`
1. 実行中のすべての[!DNL cron] ジョブを検索：`SELECT * FROM cron_schedule WHERE status = 'running';`
1. 通常より長く実行されているジョブの`job_code`をコピーします。
1. 前の手順のスケジュール IDを使用して、特定の[!DNL cron] ジョブのロックを解除します：`./vendor/bin/ece-tools cron:unlock --job-code=<job_code_1> [... --job-code=<job_code_x>]`

### 単一の[!DNL cron]を停止するためのソリューション {#solution-stop-a-single-cron}

1. ターミナルを開き、[SSH キー](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections)を使用して、影響を受ける環境に接続します。
1. 次のコマンドを使用して、長時間実行しているタスクを確認します。

   `date; ps aux | grep '[%]CPU\|cron\|magento\|queue' | grep -v 'grep\|cron -f'`

1. 以下のサンプル出力のように、出力に現在の日付とプロセスのリストが表示されます。 `START`列には、プロセスの開始時間または開始日が表示されます。

   ```
   Wed May  8 22:41:31 UTC 2019
   USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
   root       590  0.0  0.0  27528  2768 ?        Ss   Jan15   0:49 /usr/sbin/cron -f
   bxc2qly+ 25855  0.0  0.0  23724  2184 ?        S    20:51   0:00 logger -d -u /run/bxc2qlykqhbqe_stg-cron.sock -p cron.info -s -t cron-bxc2qlykqhbqe_stg-bxc2qlykqhbqe_stg
   bxc2qly+ 25860 57.7  1.3 584220 222692 ?       S    20:51   0:02 php bin/magento cron:run
   bxc2qly+ 25863  0.0  0.0  23724  2472 ?        S    20:51   0:00 logger -d -u /run/bxc2qlykqhbqe-cron.sock -p cron.info -s -t cron-bxc2qlykqhbqe-bxc2qlykqhbqe
   bxc2qly+ 25876 53.0  0.6 475472 111468 ?       R    20:51   0:01 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe_stg/bin/magento cron:run --group=index --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25878 57.0  0.6 475472 112080 ?       R    20:51   0:01 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe_stg/bin/magento cron:run --group=staging --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25880 50.5  0.6 475472 111312 ?       R    20:51   0:01 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe_stg/bin/magento cron:run --group=catalog_event --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25882 48.5  0.6 475472 111220 ?       R    20:51   0:00 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe_stg/bin/magento cron:run --group=consumers --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25884 50.5  0.6 475472 111372 ?       R    20:51   0:01 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe_stg/bin/magento cron:run --group=ddg_automation --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25890 32.5  0.6 475368 110672 ?       R    20:51   0:00 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe/bin/magento cron:run --group=staging --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25892 34.5  0.6 475472 110724 ?       R    20:51   0:00 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe/bin/magento cron:run --group=catalog_event --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25894 31.5  0.6 475368 110136 ?       R    20:51   0:00 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe/bin/magento cron:run --group=consumers --bootstrap=standaloneProcessStarted=1
   bxc2qly+ 25896 29.0  0.6 475320 109876 ?       R    20:51   0:00 /usr/bin/php7.1-zts /app/bxc2qlykqhbqe/bin/magento cron:run --group=ddg_automation --bootstrap=standaloneProcessStarted=1
   ```

1. ブロック展開プロセスを実行する可能性のある長時間実行中の[!DNL cron] ジョブが表示される場合は、`kill` コマンドを使用してプロセスを終了できます。**プロセス ID** （`PID`列が見つかりました）を特定し、その`PID`をコマンドに入れてプロセスを強制終了できます。
**kill process** コマンドは次のとおりです。

   `kill -9 <PID>`

1. 次に、再デプロイする場合は、再デプロイできます。
