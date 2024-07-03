---
title: Cron タスクは他のグループからタスクをロック
description: この記事では、特定の長時間実行される cron ジョブが他の cron ジョブをブロックすることに関連する、Adobe Commerce on cloud infrastructure の問題のソリューションを提供します。
exl-id: b5b9e8b3-373c-4f93-af9c-85da84dbc928
feature: Configuration
role: Developer
source-git-commit: faa80e8233438fc15781341b3a9d5325269d6d20
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Cron タスクは他のグループからタスクをロック

この記事では、特定の長時間実行される cron ジョブが他の cron ジョブをブロックすることに関連する、Adobe Commerce on cloud infrastructure の問題のソリューションを提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ
* 2019 年 5 月以前にオンボード

## 問題

Adobe Commerce for cloud には、複雑な cron タスク（長時間実行タスク）がある場合、他のタスクをロックして実行してしまう可能性があります。 例えば、インデクサーのタスクは、無効化されたインデクサーのインデックスを再作成します。 終了までに数時間かかる場合があり、メールの送信、サイトマップの生成、顧客通知、その他のカスタムタスクなど、他のデフォルトの cron ジョブがロックされます。

<u>症状</u>:

Cron ジョブで実行されるプロセスは実行されません。 例えば、製品のアップデートが時間に適用されない、顧客からメールが届かないと報告される、などの場合です。

を開くと `cron_schedule` データベース テーブルには、次のジョブが表示されます `missed` ステータス。

## 原因：

以前は、クラウド環境では、Jenkins サーバーを使用して cron ジョブを実行していました。 Jenkins は、一度に 1 つのジョブのインスタンスのみを実行します。その結果、1 つのジョブのみが実行されます `bin/magento cron:run` 一度に実行されるプロセス。

## 解決策

1. 連絡先 [Adobe Commerce サポート](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 自己管理 cron を有効にする。
1. を編集する `.magento.app.yaml` git ブランチのAdobe Commerce コードのルートディレクトリにあるファイル。 以下を追加します。

   ```yaml
     crons:
     cronrun:
     spec: "* * * * *"
     cmd: "php bin/magento cron:run"
   ```

1. ファイルを保存し、更新をステージング環境と実稼動環境にプッシュします（統合環境で行う場合と同じ方法）。

>[!NOTE]
>
>複数ある場合、古い cron 設定を転送する必要はありません `cron:run` 新しい cron スケジュールに存在（通常 `cron:run` 上記のように追加されたタスクで十分です。 ただし、カスタムジョブがある場合は、転送する必要があります。

### 自己管理の cron が有効になっているかどうかを確認します（Cloud Pro ステージングおよび実稼動環境の場合のみ）。

自己管理 Cron が有効かどうかを確認するには、 `crontab -l` コマンドを実行し、結果を確認します。

* 自己管理 Cron が有効になっていることを確認できます。次のようなタスクが表示されます。

  ```bash
  username@hostname:~$ crontab -l    # Crontab is managed by the system, attempts to edit it directly will fail.
  SHELL=/etc/platform/username/cron-run    MAILTO=""    # m h dom mon dow job_name    * * * * * cronrun
  ```

* タスクを表示して取得できない場合、自己管理 cron は有効になっていません *「このプログラムは使用できません」* エラーメッセージ。

>[!NOTE]
>
>自己管理 cron が有効かどうかを確認する上記のコマンドは、スタータープランおよび開発/統合環境には適用されません。

## 関連資料

* [cron ジョブの設定](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) 開発者向けドキュメントを参照してください。
