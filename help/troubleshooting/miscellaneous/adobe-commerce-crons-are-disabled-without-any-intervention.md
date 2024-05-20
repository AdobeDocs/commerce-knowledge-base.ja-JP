---
title: Adobe Commerce [!DNL crons] 介入なしで無効にされた
description: この記事を使用して、次の問題を修正します [!DNL crons] は操作なしで無効になります。
exl-id: 5172d2ae-53ad-4db6-ae00-7b27c96911e9
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Adobe Commerce Cron が操作なしで無効化される

この記事では、次のような場合のソリューションを提供します [!DNL crons] は操作なしで無効になります。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf).

## 問題

あなたの [!DNL crons] デプロイメント後は無効になります。

<u>再現手順</u>:

デプロイ。

<u>期待される結果</u>:

あなたの [!DNL crons] 実行中です。

<u>実際の結果</u>:

あなたの [!DNL crons] デプロイメント後は無効になります。

## 原因：

の問題 [!DNL OPcache] 設定。

## 解決策

アップグレード [!DNL ECE Tools] を最新バージョンに更新します [2002.1.13](https://devdocs.magento.com/cloud/release-notes/ece-release-notes.html#v2002113).

## 関連資料

* [パフォーマンスが遅く、実行速度が遅く、実行時間が長い [!DNL crons]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.html) サポートナレッジベースで。
* [[!DNL Cron] タスクは他のグループからタスクをロックします](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html?lang=en) サポートナレッジベースで。
* [[!DNL Cron] ジョブが「実行中」ステータスで停止する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html?lang=en) サポートナレッジベースで。
