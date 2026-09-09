---
title: Adobe Commerce [!DNL crons] は操作なしでは無効になっています
description: この記事を使用して、介入なしで [!DNL crons] が無効になる問題を修正します。
exl-id: 5172d2ae-53ad-4db6-ae00-7b27c96911e9
source-git-commit: 6bff1d7a0578ceb8ea17dff347b1bcd4f0068e7a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Adobe Commerce cronsを操作せずに無効にする

この記事では、[!DNL crons]が介入せずに無効になっている場合の解決策を紹介します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、すべての[&#x200B; サポートされているバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)。

## イシュー

デプロイメント後に[!DNL crons]は無効になります。

<u>複製する手順</u>:

展開。

<u>期待される結果</u>:

[!DNL crons]が実行中です。

<u>実際の結果</u>:

デプロイメント後に[!DNL crons]は無効になります。

## 原因

[!DNL OPcache]設定に関する問題。

## Solution

[!DNL ECE Tools]を最新バージョン [2002.1.13](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/release-notes/ece-tools-package#v2002113)にアップグレードします。

## 関連トピックス

* [&#x200B; パフォーマンスが遅く、実行が遅く、長時間実行されています [!DNL crons]](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-42802) （サポートナレッジベース）。
* [[!DNL Cron]  タスクは、サポート ナレッジベースの他のグループ &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html?lang=ja)からタスクをロックします。
* [[!DNL Cron]  ジョブがサポートナレッジベースの「実行中」ステータス &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html?lang=ja)で停止しています。
