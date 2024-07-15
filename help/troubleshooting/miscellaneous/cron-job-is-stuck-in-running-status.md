---
title: 「ジョブ [!DNL Cron]**実行中**ステータスで停止している」
description: この記事では、Adobe Commerce [!DNL cron] jobs が実行中を終了せず、「実行中」ステータスのままになり、他のジョブが実行できなくなる場合のソリュ  [!DNL cron]  ションについて説明します。 これは、ネットワークの問題、アプリケーションのクラッシュ、再デプロイメントの問題など、様々な理由で発生する可能性があります。
exl-id: 11e01a2b-2fcf-48c2-871c-08f29cd76250
feature: Configuration
role: Developer
source-git-commit: 08a241131453725a86eda5f267a209e6705da2e3
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# ジョブ [!DNL Cron] 「実行中」ステータスでスタックしています

この記事では、Adobe Commerce [!DNL cron] ジョブが実行中で終了せず、「実行中」ステータスのままになり、他の [!DNL cron] ジョブが実行できなくなる場合の解決策について説明します。 これは、ネットワークの問題、アプリケーションのクラッシュ、再デプロイメントの問題など、様々な理由で発生する可能性があります。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 症状 {#symptom}

リセットが必要なジョブ [!DNL cron] 症状は次のとおりです。

* 大量のジョブが `cron_schedule` キューに表示されます
* サイトのパフォーマンスが低下し始める
* ジョブがスケジュールどおりに実行できない

## 解決策 {#solutions}

### すべての [!DNL cron] ジョブを一度に停止するソリューション {#solution-stop-all-crons-at-once}

>[!WARNING]
>
>`--job-code` オプションを指定せずにこのコマンドを実行すると、現在実行中のジョブを含め、*すべて* の [!DNL cron] ジョブがリセットされます。そのため、すべての [!DNL cron] ジョブをリセットする必要があることを確認した後など、例外的な場合にのみ使用することをお勧めします。 再デプロイメントでは、デフォルトでこのコマンドを実行してジョブ [!DNL cron] リセットするので、環境がバックアップされた後に適切に回復されます。 インデクサーを実行している場合は、この解決策を使用しないでください。

この問題を解決するには、`cron:unlock` コマンドを使用して [!DNL cron] ジョブをリセットする必要があります。 このコマンドは、データベース内の [!DNL cron] ジョブのステータスを変更し、ジョブを強制的に終了して、他のスケジュールされたジョブを続行できるようにします。

1. ターミナルを開き、[SSH キー ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections) を使用して、影響を受ける環境に接続します。
1. MySQL データベース資格情報を取得します。    ```shell    echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp    ```
1. `mysql` を使用してデータベースに接続します。    ```shell    mysql -hdatabase.internal -uuser -ppassword main    ```
1. `main` データベースを選択します。    ```shell    use main    ```
1. 実行中のすべての [!DNL cron] ジョブを検索します：    ```shell    SELECT * FROM cron_schedule WHERE status = 'running';    ```
1. 通常よりも長時間実行されているジョブの `job_code` をコピーします。
1. 前の手順のスケジュール ID を使用して、特定の [!DNL cron] ジョブのロックを解除します。    ```shell    ./vendor/bin/ece-tools cron:unlock --job-code=<job_code_1> [... --job-code=<job_code_x>]    ```

### 単一の [!DNL cron] を停止するソリューション {#solution-stop-a-single-cron}

1. ターミナルを開き、[SSH キー ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections) を使用して、影響を受ける環境に接続します。
1. 次のコマンドを使用して、長時間実行されているタスクを確認します。

   ```date; ps aux | grep '[%]CPU\|cron\|magento\|queue' | grep -v 'grep\|cron -f'```

1. 以下のサンプル出力のように、出力には現在の日付とプロセスのリストが表示されます。 `START` の列には、プロセスの開始時刻または日付が表示されます。

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

1. デプロイメントプロセスがブロックされる可能性のある長時間実行中の [!DNL cron] ジョブが表示された場合は、`kill` コマンドを使用してプロセスを終了できます。 **プロセス ID** （`PID` 列が見つかりました）を特定し、その `PID` をコマンドに配置してプロセスを強制終了できます。
**kill process** コマンドは次のとおりです。

   ```kill -9 <PID>```

1. 再デプロイしようとした場合は、再デプロイできます。
