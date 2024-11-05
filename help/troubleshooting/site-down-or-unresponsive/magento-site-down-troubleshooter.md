---
title: Adobe Commerce サイトの停止に関するトラブルシューティング
description: 各質問をクリックすると、トラブルシューティングの各ステップの回答の詳細が表示されます。
exl-id: 10a2313e-cc82-4ffc-9247-624884f3e165
feature: Support
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Adobe Commerce サイトの停止に関するトラブルシューティング

各質問をクリックすると、トラブルシューティングの各ステップの回答の詳細が表示されます。

## 手順 1 {#step-1}

+++**問題 <https://status.adobe.com> 表示されますか？**

回答：はい。[Adobe Commerceのステータス ](https://status.adobe.com/cloud/experience_cloud) をチェックして問題が発生した場合は、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開いて詳細を確認してください。\
b.いいえ – [Adobe Commerceのステータス ](https://status.adobe.com/cloud/experience_cloud) をオンにしたが、問題が表示されなかった場合は、[ 手順 2](#step-2) に進んでください。

+++

## 手順 2 {#step-2}

+++**http://status.fastly.comに何か問題はありますか？**

a.はい。[[!DNL Fastly]  ステータス ](https://status.fastly.com/) をチェックして問題が発生した場合は、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開いて詳細を確認します。\
b.いいえ – [[!DNL Fastly]  ステータス ](https://status.fastly.com/) をオンにしたが、問題が表示されなかった場合は、[ 手順 3](#step-3) に進みます。

+++

## 手順 3 {#step-3}

+++**Web ブラウザーで web サイトを確認します。 200 （OK）のコードは出ますか？**

**Firefox** でエラーコードを確認するには、**メニューを開く** アイコン/**Web Developer**/**ツールを切り替え**/**ネットワーク** タブ/**すべて** フィルター/**ステータス** 列をクリックします。 **Chrome** のエラーコードを確認するには、**[ 開く ] メニュー** アイコン/**その他のツール**/**デベロッパーツール**/**ネットワーク** タブ/**すべて** フィルター/**ステータス** 列をクリックします。

a.はい。詳細な調査のために [ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開きます。\
b.いいえ – [ 手順 4](#step-4) に進みます。

+++

## 手順 4 {#step-4}

+++**受け取った Web サイトエラーコード**

a. エラーコード 500 - `/var/log/platform/` のログを確認します。 このデータで問題が見つからない場合は、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開いて、現在までのトラブルシューティング情報を含め、さらに調査することができます。

b. エラーコード 503 - `var/reports` のログを確認します。 このデータで問題が見つからない場合は、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開いて、現在までのトラブルシューティング情報を含め、さらに調査することができます。

c. エラーコード 404 – 次のクエリを実行します。`SELECT f.flag_data->>'$.current_version' as flag_version, (su.id IS NOT NULL) as update_exists FROM flag f LEFT JOIN staging_update su ON su.id = f.flag_data->>'$.current_version' WHERE flag_code = 'staging';` クエリでテーブルが返され、`update_exists` の値が「0」の場合は、[ コンテンツのステージングに関する問題が原因で、すべてのページ、ストアフロントおよび管理者の Error 404](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/site-down-or-unresponsive/error-404-on-all-pages-due-to-content-staging-issue) の記事を参照してください。 それ以外の場合は、[ 手順 5](#step-5) に進みます。

d.その他のエラーコード - [ 手順 5](#step-5) に進みます。

+++

## 手順 5 {#step-5}

+++**サイトが遅い、またはサーバー負荷が高い、CPU 負荷が高い、リクエスト処理が遅い、または [!DNL MySQL] や Redis が停止している**。

回答：はい。[CLI からの DDOS 攻撃のチェック ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli) の手順を進めます。\
b.いいえ – `/var/log/exception.log` と `/var/log/deploy.log` のログを確認して、このデータで問題が見つからない場合は、[ 手順 6](#step-6) に進んでください。

+++

## 手順 6 {#step-6}

+++**デプロイメントエラーまたはデプロイメントエラーはありますか？**

a.はい – [ 手順 13](#step-13) に進みます。\
b.いいえ – [ 手順 7](#step-7) に進みます。

+++

## 手順 7 {#step-7}

+++**Elasticsearchエラーはありますか？**

a.はい – [Elasticsearchの確認 ](https://developer.adobe.com/commerce/php/module-reference/module-elasticsearch/) 手順に進みます。\
b.いいえ – [ 手順 8](#step-8) に進みます。

+++

## 手順 8 {#step-8}

+++**[!DNL MySQL] データベースで低速のクエリや誤ったクエリが発生していましたか？**

回答：はい。[ 処理に時間のかかるクエリとプロセスの確認に時間がかかりすぎるクエリのチュートリアル ](https://dev.mysql.com/doc/refman/5.5/en/entering-queries.html) を続  [!DNL MySQL]](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql) and checking your query structure in this [[!DNL MySQL]  ます。\
b.いいえ – [ 手順 9](#step-9) に進みます。

+++

## 手順 9 {#step-9}

+++**静的コンテンツは使用できませんか？**

a.はい。[ 静的コンテンツの確認 ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment) の記事を参照して進みます。\
b.いいえ – [ 手順 10](#step-10) に進みます。

+++

## 手順 10 {#step-10}

+++**ログに PHP Fatal エラーが表示されますか？**

a.はい – コンサルティング [ 一般的な PHP の致命的なエラーと解決策 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/common-php-fatal-errors-and-solutions) を続行します。\
b.いいえ – [ 手順 11](#step-11) に進みます。

+++

## 手順 11 {#step-11}

+++**Redis エラーが表示されますか？**

a.はい – 手順に進んで [ 実行中であることを確認  [!DNL Redis] ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/redis#troubleshooting-redis) および [[!DNL Redis]  トラブルシューティング ](https://redis.io/topics/problems) を行います。\
b.いいえ – [ 手順 12](#step-12) に進みます。

+++

## 手順 12 {#step-12}

+++**インデクサーエラーが発生していますか？**

回答：はい。インデックスが別のプロセスによってロックされている場合は、を参照してください [ インデックスが別のプロセスによってロックされています ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/index-is-locked-by-another-process)。 その他のインデクサーエラーがある場合は、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開いて詳細を確認してください。\
b.いいえ。詳細な調査のために [ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開きます。

+++

## 手順 13 {#step-13}

+++**カスタムモジュールに問題がありますか？**

a.はい – [ 一般的なカスタムモジュールのトラブルシューティングヘルプ ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/general-custom-module-troubleshooting-help) を参照してください。\
b.いいえ – [ 手順 14](#step-14) に進みます。

+++

## 手順 14 {#step-14}

+++**フック後のエラーはありますか？**

a.はい – この [[!DNL MySQL]  サーバーエラーメッセージ リファレンス ](https://dev.mysql.com/doc/mysql-errors/5.7/en/server-error-reference.html) で [!DNL MySQL] エラーを確認して進みます。\
b.いいえ – [ 手順 15](#step-15) に進みます。

+++

## 手順 15 {#step-15}

+++**composer パッチに関する問題はありますか？**

a.はい – コンサルティングに進みます [ パッチを適用すると、サイトがダウンします ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/site-down-or-unresponsive/applying-a-patch-takes-your-site-down)。\
b.いいえ – [ 手順 16](#step-16) に進みます。

+++

## 手順 16 {#step-16}

+++**SQL データベースエラーはありますか？**

a.はい – この [[!DNL MySQL]  サーバーエラーメッセージ リファレンス ](https://dev.mysql.com/doc/mysql-errors/5.7/en/server-error-reference.html) で [!DNL MySQL] エラーを確認して進みます。\
b.いいえ – [ 手順 17](#step-17) に進みます。

+++

## 手順 17 {#step-17}

+++**データベース [!DNL MySQL] デッドロックまたは応答しない [!DNL MySQL] データベースがありますか？**

回答：はい。この [ デッドロックの [!DNL MySQL] の記事で、デッドロックの確認を続行し  [!DNL MySQL]](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/database/deadlocks-in-mysql) ください。\
b.いいえ。詳細な調査のために [ サポートチケット ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) を開きます。

+++

[手順 1 に戻る](#step-1)

サイトダウントラブルシューティングのフローチャートを表示するには、[ ここ ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/site-down-or-unresponsive/site-down-troubleshooting-diagram) をクリックしてください。

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
