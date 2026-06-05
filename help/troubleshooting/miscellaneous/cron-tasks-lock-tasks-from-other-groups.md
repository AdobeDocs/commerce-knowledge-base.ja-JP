---
title: '[!DNL Cron]件のタスクが他のグループからタスクをロックしています'
description: この記事では、特定の長時間実行 [!DNL cron]  ジョブが他 [!DNL cron]  ジョブをブロックすることに関連するAdobe Commerce on cloud infrastructureの問題に対する解決策を提供します。
exl-id: b5b9e8b3-373c-4f93-af9c-85da84dbc928
feature: Configuration
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# [!DNL Cron]件のタスクが他のグループからタスクをロックしています

この記事では、他の[!DNL cron]件のジョブをブロックする特定の長期的な[!DNL cron]件のジョブに関連するAdobe Commerce on cloud infrastructureの問題に対する解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure Pro プランアーキテクチャ
* 2019年5月以前のオンボーディング

## イシュー

Adobe Commerce クラウド版では、複雑な[!DNL cron]個のタスク（長期実行タスク）がある場合、実行のために他のタスクがロックされる可能性があります。 例えば、インデクサーのタスクは、無効なインデクサーを再インデックスします。 完了までに数時間かかる場合があり、電子メールの送信、サイトマップの生成、顧客通知、その他のカスタムタスクなど、デフォルトの[!DNL cron] ジョブがロックされます。

<u>症状</u>:

[!DNL cron] ジョブによって実行されたプロセスは実行されません。 例えば、製品のアップデートは何時間も適用されないか、顧客がメールを受信していないと報告します。

`cron_schedule` データベース テーブルを開くと、`missed` ステータスのジョブが表示されます。

## 原因

以前、私たちのクラウド環境では、Jenkins サーバーを使用して[!DNL cron] ジョブを実行していました。 Jenkinsは、一度に1つのジョブのインスタンスのみを実行します。その結果、一度に1つの`bin/magento cron:run` プロセスのみが実行されます。

## Solution

1. [Adobe Commerce サポート &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)に連絡して、セルフマネージド [!DNL crons]を有効にしてください。
1. [!DNL Git] ブランチのAdobe Commerce コードのルート ディレクトリにある`.magento.app.yaml` ファイルを編集します。 以下を追加します。

   ```yaml
     crons:
     cronrun:
     spec: "* * * * *"
     cmd: "php bin/magento cron:run"
   ```

1. ファイルを保存し、ステージング環境と実稼動環境に更新をプッシュします（統合環境と同じ方法で）。

>[!NOTE]
>
>複数の`cron:run`が存在する古い[!DNL cron]設定を新しい[!DNL cron] スケジュールに転送する必要はありません。上記のように追加された通常の`cron:run` タスクで十分です。 ただし、カスタムジョブがある場合は、それを転送する必要があります。

### セルフマネージド [!DNL cron]が有効になっているかどうかを確認します（Cloud Pro ステージングおよび実稼動環境のみ）

自己管理型[!DNL cron]が有効かどうかを確認するには、`crontab -l` コマンドを実行し、結果を確認します。

* 次のようなタスクを表示できる場合は、自己管理[!DNL cron]が有効になります。

  ```bash
  username@hostname:~$ crontab -l    # Crontab is managed by the system, attempts to edit it directly will fail.
  SHELL=/etc/platform/username/cron-run    MAILTO=""    # m h dom mon dow job_name    * * * * * cronrun
  ```

* タスクが表示されず、*「このプログラムを使用できません」というエラーメッセージが表示された場合、自己管理[!DNL cron]は有効になっていません。*

>[!NOTE]
>
>自己管理[!DNL cron]が有効になっているかどうかを確認する上記のコマンドは、スタータープランおよび開発/統合環境には適用されません。

## 関連トピックス

* 開発者ドキュメントの[&#x200B; セットアップ  [!DNL cron]  ジョブ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
