---
title: が無効になった理由  [!DNL cron]  確認方法
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceの cron に関する問題のトラブルシューティングソリューションについて説明します。
feature: Configuration
role: Developer
exl-id: d4d4a28d-3afa-4379-afc1-bc6250717784
source-git-commit: c5e94c6407394cd905ea470628d28db2c2c6c0ed
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!DNL cron] が無効になった理由を確認する方法

この記事では、クラウドインフラストラクチャー上のAdobe Commerceの [!DNL cron] に関する問題のトラブルシューティングソリューションを提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

## [!DNL cron] の問題の症状を次に示します。

[!DNL cron] が実行されていないことに気がつきました。
例：`app/etc/env.php` ファイルに次の行が表示されます。

```'cron' =>
  array (
    'enabled' => 0
  ),
```

空の配列は、[!DNL cron] が **有効** であることを意味します。

```'cron' =>
  array (
  ),
```

## 原因

[!DNL cron] が現在アクティブではない理由はいくつかあります。

1. [!DNL OpCache] 設定が見つからなかったため、[!DNL cron] は無効になりました。
1. [!DNL cron] イトのパフォーマンスが低下したり利用停止になったりしたため、インフラストラクチャ チームがサイトを無効にしました。
1. デプロイメントに失敗したので、[!DNL cron] は再度有効になりませんでした。

問題の解決策については、次のいずれかの節を参照してください。

## 解決策

### [!DNL OpCache] 設定の欠落の解決策 {#solution-missed-opcache-settings}

Commerce ナレッジベースの [[!DNL Cron]  設定の誤りまたは欠落  [!DNL OpCache]  設定が原因で停止 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/crons-blocked-running-missing-opache-settings) を参照してください。

### インフラストラクチャチームによる無効化向けソリューション {#solution-disabled-by-infrastructure-team}

1. サイトがダウンしているか、応答していない以前のサポートチケットを確認します。
1. 次に、インフラストラクチャチームが無効にしたことを示したかどうかを確認します。
1. インフラストラクチャチームによって発生した問題や懸念に対処したことを確認します。
1. さらにサポートが必要な場合は [ サポートリクエスト ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-tickets) を送信し、[!DNL cron] を再度有効にして、インフラストラクチャチームが示した問題に対処する方法を説明するようリクエストします。

### 展開用のソリューションが失敗しました {#solution-deployment-failed}

デプロイメントログを確認します。

* Commerce on Cloud Infrastructure ガイドの [ ログの表示と管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations)。
* Commerce ナレッジベースの [Cloud UI にエラーがあ *`log snipped`* 場合のデプロイメントログの確認 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error)。

1. `setup:upgrade` の手順でデプロイメントが失敗した場合、[!DNL cron] は再度有効になりません。
例：デプロイメントログには、次の行が表示されます。

   ```The command "/bin/bash -c "set -o pipefail; php ./bin/magento setup:upgrade --keep-generated --ansi --no-interaction  | tee -a /app/$<project_id>/var/log/install_upgrade.log"" failed. Cache types config flushed successfully```

1. そうしないと、別のステージでデプロイメントが失敗した可能性があります。 デプロイメントログを確認し、両方の行が表示されていることを確認します（以下の例）。 ログに以下のような行が両方とも表示されない場合は、[!DNL cron] が再度有効になっていなかったことを意味します。

   ```  [2024-03-06T10:55:39.345564+00:00] INFO: Disable cron```<br>
...<br>
   ```  [2024-02-07T10:50:09.579005+00:00] INFO: Enable cron```

**さらにサポートが必要な場合は [ サポートリクエスト ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-tickets) を送信します。**
