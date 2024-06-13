---
title: Adobe Commerce サイトの停止に関するトラブルシューティング
description: 各質問をクリックすると、トラブルシューティングの各ステップの回答の詳細が表示されます。
exl-id: 10a2313e-cc82-4ffc-9247-624884f3e165
feature: Support
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Adobe Commerce サイトの停止に関するトラブルシューティング

各質問をクリックすると、トラブルシューティングの各ステップの回答の詳細が表示されます。

## 手順 1 {#step-1}

+++**実行 <https://status.adobe.com> 問題を表示しますか？**

a.はい – オンにした場合 [AdobeMagentoステータス](https://status.adobe.com/products/3350) 問題が発生しました。を開きます [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらなる調査のために。\
b. NO - オンにした場合 [AdobeMagentoステータス](https://status.adobe.com/products/3350) 問題が発生しませんでした。次の手順に進みます [手順 2](#step-2).

+++

## 手順 2 {#step-2}

+++**http://status.fastly.comに何か問題がありますか？**

a.はい – オンにした場合 [Fastly ステータス](https://status.fastly.com/) 問題が発生しました。を開きます [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらなる調査のために。\
b. NO - オンにした場合 [Fastly ステータス](https://status.fastly.com/) 問題が発生しませんでした。次の手順に進みます [手順 3](#step-3).

+++

## 手順 3 {#step-3}

+++**Web ブラウザーで web サイトを確認します。 200 （OK）のコードは出ますか？**

のエラーコードを確認するには **Firefox**：をクリックします **メニューを開く** アイコン > **Web 開発者** > **ツールの切り替え** > **ネットワーク** タブ > **すべて** フィルター > **ステータス** 列。 のエラーコードを確認するには **Chrome**：をクリックします **メニューを開く** アイコン > **その他のツール** > **開発者ツール** > **ネットワーク** タブ > **すべて** フィルター > **ステータス** 列。

a.はい – を開く [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらなる調査のために。\
b.いいえ – に進みます。 [手順 4](#step-4).

+++

## 手順 4 {#step-4}

+++**どの web サイトエラーコードを受け取りましたか？**

a. エラーコード 500 - ログを確認します。 `/var/log/platform/`. このデータで問題が発生しない場合は、 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらに調査を進めるために、これまでに入手したトラブルシューティング情報を含めます。

b. エラーコード 503 - ログを確認します。 `var/reports`. このデータで問題が発生しない場合は、 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらに調査を進めるために、これまでに入手したトラブルシューティング情報を含めます。

c. エラーコード 404 – 次のクエリを実行します。 `SELECT f.flag_data->>'$.current_version' as flag_version, (su.id IS NOT NULL) as update_exists FROM flag f LEFT JOIN staging_update su ON su.id = f.flag_data->>'$.current_version' WHERE flag_code = 'staging';` クエリがテーブルを返す場合、次の条件を満たす必要があります `update_exists` 値は「0」です。を参照してください [コンテンツのステージングに問題があるため、すべてのページ、ストアフロントおよび管理者でエラー 404 が発生する](/help/troubleshooting/site-down-or-unresponsive/error-404-on-all-pages-due-to-content-staging-issue.md) 記事。 それ以外の場合は、次の手順に従います。 [手順 5](#step-5).

d.その他のエラーコード – 次に進みます [手順 5](#step-5).

+++

## 手順 5 {#step-5}

+++**MySQL または Redis で、サイトが遅い、またはサーバー負荷が高い、CPU 負荷が高い、リクエスト処理が遅い、または停止している？**

a.はい – の手順を続行します [CLI からの DDOS 攻撃の確認](/help/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.md).\
b.いいえ – ログを確認します `/var/log/exception.log` および `/var/log/deploy.log`このデータで問題が発生しない場合は、に進んでください。 [手順 6](#step-6).

+++

## 手順 6 {#step-6}

+++**デプロイメントエラーまたはデプロイメントエラーはありますか？**

a.はい – に進みます。 [手順 13](#step-13).\
b.いいえ – に進みます。 [手順 7](#step-7).

+++

## 手順 7 {#step-7}

+++**Elasticsearchに誤りがありますか？**

a.はい – の手順を続行します [Elasticsearchの確認](https://devdocs.magento.com/guides/v2.3/config-guide/elasticsearch/configure-magento.html).\
b.いいえ – に進みます。 [手順 8](#step-8).

+++

## 手順 8 {#step-8}

+++**MySQL データベースで低速のクエリや誤ったクエリが発生していましたか？**

a.はい – 次に進みます。 [MySQL での低速クエリとプロセスの確認に時間がかかりすぎる](/help/troubleshooting/database/checking-slow-queries-and-processes-mysql.md) こちらのクエリ構造を確認しています [MySQL クエリのチュートリアル](https://dev.mysql.com/doc/refman/5.5/en/entering-queries.html).\
b.いいえ – に進みます。 [手順 9](#step-9).

+++

## 手順 9 {#step-9}

+++**静的なコンテンツは使用できませんか？**

a.はい – 次のコンサルティングに進みます [静的コンテンツの確認](https://support.magento.com/hc/en-us/articles/360031624091) 記事。\
b.いいえ – に進みます。 [手順 10](#step-10).

+++

## 手順 10 {#step-10}

+++**ログに PHP Fatal Errors が記録されていますか？**

a.はい – コンサルティングに進みます。 [一般的な PHP の致命的なエラーと解決策](/help/troubleshooting/miscellaneous/common-php-fatal-errors-and-solutions.md).\
b.いいえ – に進みます。 [手順 11](#step-11).

+++

## 手順 11 {#step-11}

+++**Redis エラーが表示されますか？**

a.はい – 次の手順に進みます [redis が実行中であることを確認します。](https://devdocs.magento.com/guides/v2.3/config-guide/redis/redis-session.html#redis-verify) および [Redis トラブルシューティング](https://redis.io/topics/problems).\
b.いいえ – に進みます。 [手順 12](#step-12).

+++

## 手順 12 {#step-12}

+++**インデクサーエラーが発生していますか？**

a.はい。インデックスが別のプロセスによってロックされている場合は、を参照してください。 [インデックスは別のプロセスによってロックされています](/help/troubleshooting/miscellaneous/index-is-locked-by-another-process.md). 他にインデクサーエラーがある場合は、を開いてください。 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらなる調査のために。\
b.いいえ – 開く [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらなる調査のために。

+++

## 手順 13 {#step-13}

+++**カスタムモジュールに問題がありますか？**

a.はい – 次の問い合わせに進みます [一般的なカスタムモジュールのトラブルシューティングヘルプ](/help/troubleshooting/miscellaneous/general-custom-module-troubleshooting-help.md).\
b.いいえ – に進みます。 [手順 14](#step-14).

+++

## 手順 14 {#step-14}

+++**フック後のエラーはありますか？**

a.はい – この MySQL エラーの確認を続行します [MySQL サーバーのエラーメッセージのリファレンス](https://dev.mysql.com/doc/mysql-errors/5.7/en/server-error-reference.html).\
b.いいえ – に進みます。 [手順 15](#step-15).

+++

## 手順 15 {#step-15}

+++**composer パッチに関する問題はありますか。**

a.はい – コンサルティングに進みます。 [パッチを適用すると、サイトが停止します](/help/troubleshooting/site-down-or-unresponsive/applying-a-patch-takes-your-site-down.md).\
b.いいえ – に進みます。 [手順 16](#step-16).

+++

## 手順 16 {#step-16}

+++**SQL データベース・エラーはありますか。**

a.はい – この MySQL エラーの確認を続行します [MySQL サーバーのエラーメッセージのリファレンス](https://dev.mysql.com/doc/mysql-errors/5.7/en/server-error-reference.html).\
b.いいえ – に進みます。 [手順 17](#step-17).

+++

## 手順 17 {#step-17}

+++**MySQL データベースのデッドロックや応答しない MySQL データベースはありますか？**

a.はい – これで MySQL のデッドロックを確認します [MySQL のデッドロック](/help/troubleshooting/database/deadlocks-in-mysql.md) 記事。\
b.いいえ – 開く [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) さらなる調査のために。

+++

[手順 1 に戻る](#step-1)

クリック [こちら](/help/troubleshooting/site-down-or-unresponsive/site-down-troubleshooting-diagram.md) サイトダウンのトラブルシューティングのフローチャートを確認します。
