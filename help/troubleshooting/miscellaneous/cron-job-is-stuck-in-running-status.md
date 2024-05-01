---
title: “[!DNL Cron] ジョブが**実行中**ステータス」で停止する
description: この記事では、Adobe Commerceを使用する場合のソリューションを提供します [!DNL cron] ジョブは実行を完了せず、「実行中」ステータスのままになるため、他の操作ができなくなる [!DNL cron] ジョブを実行中です。 これは、ネットワークの問題、アプリケーションのクラッシュ、再デプロイメントの問題など、様々な理由で発生する可能性があります。
exl-id: 11e01a2b-2fcf-48c2-871c-08f29cd76250
feature: Configuration
role: Developer
source-git-commit: 08a241131453725a86eda5f267a209e6705da2e3
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Cron] ジョブが「実行中」ステータスで停止する

この記事では、Adobe Commerceを使用する場合のソリューションを提供します [!DNL cron] ジョブは実行を完了せず、「実行中」ステータスのままになるため、他の操作ができなくなる [!DNL cron] ジョブを実行中です。 これは、ネットワークの問題、アプリケーションのクラッシュ、再デプロイメントの問題など、様々な理由で発生する可能性があります。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 症状 {#symptom}

症状 [!DNL cron] リセットする必要があるジョブは次のとおりです。

* 大量のジョブがに表示される `cron_schedule` キュー
* サイトのパフォーマンスが低下し始める
* ジョブがスケジュールどおりに実行できない

## 解決策 {#solutions}

### すべてを停止するソリューション [!DNL cron] 一度にジョブ {#solution-stop-all-crons-at-once}

>[!WARNING]
>
>を使用せずにこのコマンドを実行 `--job-code` オプションのリセット *all* [!DNL cron] 現在実行中のものを含むジョブなので、そのすべてを確認した後など、例外的な場合にのみ使用することをお勧めします [!DNL cron] ジョブはリセットする必要があります。 再デプロイメントでは、デフォルトでこのコマンドを実行してリセットします [!DNL cron] ジョブを使用すると、環境がバックアップされた後に適切に回復します。 インデクサーを実行している場合は、この解決策を使用しないでください。

この問題を解決するには、をリセットする必要があります [!DNL cron] を使用したジョブ `cron:unlock` コマンド。 このコマンドは、 [!DNL cron] データベース内のジョブ。他のスケジュールされたジョブを続行できるようにジョブを強制的に終了します。

1. ターミナルを開き、 [SSH キー](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections) 対象の環境に接続します。
1. MySQL データベース資格情報を取得します。    ```shell    echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp    ```
1. を使用してデータベースに接続します `mysql` :    ```shell    mysql -hdatabase.internal -uuser -ppassword main    ```
1. 「」を選択します `main` データベース：    ```shell    use main    ```
1. 実行中のすべてを検索 [!DNL cron] ジョブ：    ```shell    SELECT * FROM cron_schedule WHERE status = 'running';    ```
1. をコピーします `job_code` 通常より長く実行されているジョブのリスト。
1. 前の手順のスケジュール ID を使用して、特定の ID のロックを解除します [!DNL cron] ジョブ：    ```shell    ./vendor/bin/ece-tools cron:unlock --job-code=<job_code_1> [... --job-code=<job_code_x>]    ```

### シングルを停止する場合の解決策 [!DNL cron] {#solution-stop-a-single-cron}

1. ターミナルを開き、 [SSH キー](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections) 対象の環境に接続します。
1. 次のコマンドを使用して、長時間実行されているタスクを確認します。

   ```date; ps aux | grep '[%]CPU\|cron\|magento\|queue' | grep -v 'grep\|cron -f'```

1. 以下のサンプル出力のように、出力には現在の日付とプロセスのリストが表示されます。 この `START` 列には、プロセスの開始時刻または日付が表示されます。

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

1. 長時間実行されている場合 [!DNL cron] デプロイメントプロセスをブロックする可能性のあるジョブは、を使用してプロセスを終了できます `kill` コマンド。 を識別できます **プロセス ID** （が見つかりました `PID` （列）に追加します `PID` コマンドでプロセスを強制終了します。
この **キルプロセス** コマンド：

   ```kill -9 <PID>```

1. 再デプロイしようとした場合は、再デプロイできます。
