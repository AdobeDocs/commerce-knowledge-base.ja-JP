---
title: '[!DNL Cron] タスクは他のグループからタスクをロックします'
description: この記事では、特定の長時間実行ジョブが他のジョブをブロックすることに関連した、クラウドインフラストラクチャー上のAdobe Commerceの問題  [!DNL cron]  対するソリューショ  [!DNL cron]  を説明します。
exl-id: b5b9e8b3-373c-4f93-af9c-85da84dbc928
feature: Configuration
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# [!DNL Cron] タスクは他のグループからタスクをロックします

この記事では、特定の長時間実行される [!DNL cron] ジョブが他の [!DNL cron] ジョブをブロックすることに関連する、クラウドインフラストラクチャ上のAdobe Commerceの問題のソリューションを提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ
* 2019 年 5 月以前にオンボード

## 問題

Adobe Commerce for cloud では、複雑な [!DNL cron] タスク（長時間実行タスク）がある場合、他のタスクがロックされて実行されないことがあります。 例えば、インデクサーのタスクは、無効化されたインデクサーのインデックスを再作成します。 終了までに数時間かかる場合があり、メールの送信、サイトマップの生成、顧客通知、その他のカスタムタスクなど、他のデフォルトの [!DNL cron] ジョブがロックされます。

<u> 症状 </u>:

[!DNL cron] のジョブで実行されたプロセスは実行されません。 例えば、製品のアップデートが時間に適用されない、顧客からメールが届かないと報告される、などの場合です。

`cron_schedule` データベース テーブルを開くと、`missed` の状態のジョブが表示されます。

## 原因：

以前は、クラウド環境では、[!DNL cron] ジョブの実行に Jenkins サーバーを使用していました。 Jenkins は一度に 1 つのジョブのインスタンスのみを実行します。その結果、一度に実行される `bin/magento cron:run` プロセスは 1 つだけです。

## 解決策

1. 自己管理サー [ スを有効にするには、](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)Adobe Commerce サポート [!DNL crons] にお問い合わせください。
1. `.magento.app.yaml` ブランチのAdobe Commerce コードのルートディレクトリにある [!DNL Git] ファイルを開きます。 以下を追加します。

   ```yaml
     crons:
     cronrun:
     spec: "* * * * *"
     cmd: "php bin/magento cron:run"
   ```

1. ファイルを保存し、更新をステージング環境と実稼動環境にプッシュします（統合環境で行う場合と同じ方法）。

>[!NOTE]
>
>複数の [!DNL cron] が存在する古い `cron:run` 設定を新しい [!DNL cron] スケジュールに転送する必要はありません。前述のように追加された通常の `cron:run` タスクで十分です。 ただし、カスタムジョブがある場合は、転送する必要があります。

### 自己管理 [!DNL cron] が有効になっているかどうかを確認します（Cloud Pro ステージングおよび実稼動環境の場合のみ）。

自己管理 [!DNL cron] が有効かどうかを確認するには、`crontab -l` コマンドを実行し、結果を確認します。

* 自己管理 [!DNL cron] は、次のようなタスクを表示できる場合に有効になります。

  ```bash
  username@hostname:~$ crontab -l    # Crontab is managed by the system, attempts to edit it directly will fail.
  SHELL=/etc/platform/username/cron-run    MAILTO=""    # m h dom mon dow job_name    * * * * * cronrun
  ```

* タスクが表示されず、「このプログラ [!DNL cron] を使用することはできません」というエラーメッセージが表示される場合は *自己管理* は有効になっていません。

>[!NOTE]
>
>自己管理 [!DNL cron] が有効かどうかを確認する上記のコマンドは、スタータープランおよび開発/統合環境には適用されません。

## 関連資料

* 開発者向けドキュメントの [ 設定  [!DNL cron]  ジョブ ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
