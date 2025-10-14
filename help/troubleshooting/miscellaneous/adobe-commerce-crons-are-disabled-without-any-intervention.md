---
title: 操作なし  [!DNL crons] Adobe Commerce無効
description: この記事を使用して、が介入なしに無効に  [!DNL crons]  る問題を修正します。
exl-id: 5172d2ae-53ad-4db6-ae00-7b27c96911e9
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Adobe Commerce Cron が操作なしで無効化される

この記事では、操作を行わずに [!DNL crons] を無効にする場合の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [&#x200B; サポート対象バージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)。

## 問題

デプロイ後、[!DNL crons] は無効になります。

<u> 再現手順 </u>:

デプロイ。

<u> 期待される結果 </u>:

[!DNL crons] が実行中です。

<u> 実際の結果 </u>:

デプロイ後、[!DNL crons] は無効になります。

## 原因：

[!DNL OPcache] 設定に関する問題。

## 解決策

[!DNL ECE Tools] を最新バージョン [2002.1.13](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/release-notes/ece-tools-package#v2002113) にアップグレードしてください。

## 関連資料

* [&#x200B; パフォーマンスが遅く、実行速度が遅く、実行時間が長い  [!DNL crons]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/slow-performance-slow-and-long-running-crons.html?lang=ja) というサポートナレッジベースがあります。
* サポートナレッジベースの [[!DNL Cron]  タスクは他のグループからタスクをロックします &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html?lang=ja)。
* サポートナレッジベースで [[!DNL Cron]  ジョブが「実行中」ステータス &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html?lang=ja) のままになる。
