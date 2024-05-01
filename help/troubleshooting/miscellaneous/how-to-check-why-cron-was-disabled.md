---
title: 理由の確認方法 [!DNL cron] は無効になりました
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceの cron に関する問題のトラブルシューティングソリューションについて説明します。
feature: Configuration
role: Developer
exl-id: d4d4a28d-3afa-4379-afc1-bc6250717784
source-git-commit: c5e94c6407394cd905ea470628d28db2c2c6c0ed
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 理由の確認方法 [!DNL cron] は無効になりました

この記事では、の問題のトラブルシューティングソリューションを提供します [!DNL cron] クラウドインフラストラクチャ製品のAdobe Commerceで。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

## 以下は以下の症状です。 [!DNL cron] 問題：

次のことに気付いています： [!DNL cron] は実行されていませんでした。
例えば、以下の行が表示されます。 `app/etc/env.php` ファイル：

```'cron' =>
  array (
    'enabled' => 0
  ),
```

空の配列は、 [!DNL cron] 等しい **enabled**:

```'cron' =>
  array (
  ),
```

## 原因

その理由はいくつかあります [!DNL cron] は現在アクティブではありません：

1. この [!DNL cron] がを見逃したので、は無効になりました [!DNL OpCache] 設定。
1. インフラストラクチャ チームにより、が無効になりました [!DNL cron]サイトのパフォーマンスが低下したり、機能停止になったりしたためです。
1. この [!DNL cron] デプロイメントに失敗したので、は再度有効にされませんでした。

問題の解決策については、次のいずれかの節を参照してください。

## 解決策

### ミスに対する解決策 [!DNL OpCache] 設定 {#solution-missed-opcache-settings}

参照： [[!DNL Cron] 設定の誤りや欠落により停止しました [!DNL OpCache] 設定](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/crons-blocked-running-missing-opache-settings) Commerceのナレッジベースで確認する。

### インフラストラクチャチームによる無効化向けソリューション {#solution-disabled-by-infrastructure-team}

1. サイトがダウンしているか、応答していない以前のサポートチケットを確認します。
1. 次に、インフラストラクチャチームが無効にしたことを示したかどうかを確認します。
1. インフラストラクチャチームによって発生した問題や懸念に対処したことを確認します。
1. を送信 [サポートリクエスト](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-tickets) を再度有効にするようリクエストするために追加の支援が必要な場合、 [!DNL cron] また、インフラストラクチャ・チームが示した問題にどのように対処したかを説明します。

### 展開用のソリューションが失敗しました {#solution-deployment-failed}

デプロイメントログを確認します。

* [ログの表示と管理](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations) クラウドインフラストラクチャーに関するCommerceのガイドを参照してください。
* [Cloud UI のデプロイメントログを確認しています *`log snipped`* エラー](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error) Commerceのナレッジベースで確認する。

1. 次の期間にデプロイメントが失敗した場合： `setup:upgrade` 手順、 [!DNL cron] は再度有効にはなりません。
例：デプロイメントログには、次の行が表示されます。

   ```The command "/bin/bash -c "set -o pipefail; php ./bin/magento setup:upgrade --keep-generated --ansi --no-interaction  | tee -a /app/$<project_id>/var/log/install_upgrade.log"" failed. Cache types config flushed successfully```

1. そうしないと、別のステージでデプロイメントが失敗した可能性があります。 デプロイメントログを確認し、両方の行が表示されていることを確認します（以下の例）。 このような行がログに両方とも表示されない場合は、次のことを意味します。 [!DNL cron] は再度有効になっていません：

   ```  [2024-03-06T10:55:39.345564+00:00] INFO: Disable cron```<br>
...<br>
   ```  [2024-02-07T10:50:09.579005+00:00] INFO: Enable cron```

**を送信 [サポートリクエスト](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-tickets) さらにサポートが必要な場合。**
