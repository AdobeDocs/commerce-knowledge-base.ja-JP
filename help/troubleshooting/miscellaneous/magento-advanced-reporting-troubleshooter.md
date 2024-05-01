---
title: Adobe Commerceの高度なレポートのトラブルシューティング
description: Adobe Commerceの高度なレポートの問題は、このトラブルシューティングツールを使用して解決できます。 これには、データが表示されない高度なレポートや 404 エラーが含まれます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。
exl-id: 7ef9870c-b6b6-4144-a5a7-81aa20a1606c
feature: Cache, Support
role: Developer
source-git-commit: 84b4ca4c4144381f0b404d2eae6684e7b21755df
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Adobe Commerceの高度なレポートのトラブルシューティング

Adobe Commerceの高度なレポートの問題は、このトラブルシューティングツールを使用して解決できます。 これには、データが表示されない高度なレポートや 404 エラーが含まれます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。

## 手順 1 - サイトが高度なレポート要件を満たしていることを確認する {#step-1}

+++**Web サイトは高度なレポート要件を満たしていますか。**

詳細レポートを使用すると、404 エラーページが表示される。 Web サイトは以下を満たしていますか [高度なレポート要件](https://docs.magento.com/user-guide/reports/advanced-reporting.html#requirements)?

a.はい – に進みます。 [手順 2](#step-2).\
b.いいえ – サイトの高度なレポート要件を完了するには、の手順に従ってください。 [高度なレポート要件](https://docs.magento.com/user-guide/reports/advanced-reporting.html#requirements). その後、に進みます。 [手順 2](#step-2).

+++

## 手順 2 – 複数の基本通貨での注文があるか。 {#step-2}

+++**複数の基本通貨を使用していますか？**

複数の基本通貨を（注文および設定内で）使用していますか。 次の SQL コマンドを実行して、現在の設定を取得します。 `SELECT value FROM core_config_data WHERE path = 'currency/options/base';` .

a.はい – クエリによって複数の行が返された場合、サポートされる通貨は 1 つのみなので、高度なレポートは使用できません。\
b. NO – 出力には 1 つの通貨のみが表示されます。 例： `USD`. 複数の基本通貨が（注文で）使用されたことはありますか？ 次の SQL コマンドを実行して、注文の履歴データを取得します。\
`SELECT DISTINCT base_currency_code FROM sales_order;`.
**メモ：このコマンドを使用するには、完全なテーブル スキャンが必要です。そのため、レコード数が多いテーブルの場合、クエリの実行中にパフォーマンスに影響を与える可能性があります** 履歴オーダーデータを取得する。
複数の基本通貨が使用されたことがある場合は、1 つの通貨のみをサポートしているので、高度なレポートを使用できません。 出力に 1 つの通貨のみが表示される場合は、次に進みます。 [手順 3](#step-3).

+++

## 手順 3 – 分割データベースが使用中かどうかを確認する {#step-3}

+++**スプリット・データベース・ソリューションを使用していますか。**

を使用していますか [データベース分割ソリューション](https://devdocs.magento.com/guides/v2.3/config-guide/multi-master/multi-master.html)?

a.はい – パッチを使用します **MDVA-26831** 。対象： [分割データベースソリューションの高度なレポート 404 エラー](/help/troubleshooting/known-issues-patches-attached/advanced-reporting-404-error-on-split-database-solution.md) キャッシュをクリアします。 ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。\
b.いいえ – に進みます。 [手順 4](#step-4).

+++

## 手順 4 – 詳細レポートが有効であることを確認 {#step-4}

+++**高度なレポート機能は有効になっていますか。**

チェック **Admin** > **ストア** > **設定** > **設定** > **一般** > **詳細**. 詳細な手順については、を参照してください。 [高度なレポート機能：高度なレポート機能を有効にします](https://docs.magento.com/user-guide/reports/advanced-reporting.html#step-1-enable-advanced-reporting).

a.はい – に進みます。 [手順 5](#step-5).\
b.いいえ –  [高度なレポート機能を有効にする](https://docs.magento.com/user-guide/reports/advanced-reporting.html#step-1-enable-advanced-reporting) 保存して、Adobe Commerceと詳細レポートが同期するまで 24 時間待ちます。 データが読み込まれるかどうかを確認します。 問題が解決した場合。 次の手順に進まない場合： [手順 5](#step-5).

+++

## 手順 5 - トークンの確認 {#step-5}

+++**トークンはありますか。**

次のクエリを実行して、トークンがあることを確認します。 `SELECT * FROM core_config_data WHERE path LIKE 'analytics/general/token' \G` トークンはありますか。

a.はい – に進みます。 [手順 7](#step-7).\
b.いいえ – トークンの値が NULL であるか、データベースにレコードがない場合、に進みます。 [手順 6](#step-6).

+++

## 手順 6 – 行を使用 {#step-6}

+++**クエリはローを返しますか？**

次のクエリを実行して、フラグ テーブルのカウンター値を確認してください： ``SELECT * FROM `flag` where `flag_code` = 'analytics_link_subscription_update_reverse_counter'\G`` クエリはローを返しますか？

a.はい – 次の手順を実行します。1. 次のクエリを実行します。\
``DELETE from `flag` where `flag_code` = 'analytics_link_subscription_update_reverse_counter';``\
2\. [詳細レポートモジュールの無効化および有効化](https://docs.magento.com/user-guide/reports/advanced-reporting.html#step-1-enable-advanced-reporting) 設定と [トークンを再認証](https://docs.magento.com/user-guide/reports/advanced-reporting.html#verify-that-the-integration-is-active).\
3\. Adobe Commerceと詳細レポートが同期するまで 24 時間待ちます。 詳細レポートでデータが表示されない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b.いいえ – クエリから何も返されない場合は、次の手順に従います。1. [詳細レポートモジュールの無効化および有効化](https://docs.magento.com/user-guide/reports/advanced-reporting.html#step-1-enable-advanced-reporting) 設定と [トークンを再認証](https://docs.magento.com/user-guide/reports/advanced-reporting.html#verify-that-the-integration-is-active).\
2\. Adobe Commerceと詳細レポートが同期するまで 24 時間待ちます。 詳細レポートでデータが表示されない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 7 – でのレコードの確認 `cron_schedule` テーブル {#step-7}

+++**次にレコードがあります `cron_schedule` テーブル？**

そのジョブを確認 `analytics_collect_data` は、次のクエリを実行することによって実行されました： `SELECT * FROM cron_schedule WHERE job_code LIKE 'analytics_collect_data' \G`

a.はい – レコードがあり、 **ステータス** 列のメッセージ _逃した_&#x200B;このサポート情報記事のパッチを使用します [独自の cron グループで実行するように詳細レポートを更新](/help/troubleshooting/known-issues-patches-attached/update-advanced-reporting-to-run-on-its-own-cron-group.md).\
b.はい – レコードがあり、 **ステータス** 列のメッセージ _成功_&#x200B;に進みます。 [手順 9](#step-9).\
c.はい – レコードがあり、 **ステータス** 列のメッセージ _エラー_&#x200B;に進みます。 [手順 8.](#step-8)\
d.いいえ – レコードがない場合は、に進みます。 [手順 8](#step-8).

+++

## 手順 8 - ジョブのチェックイン `support_report.log` {#step-8}

+++**ジョブはログイン中か `support_report.log`?**

次のコマンドを実行します。 `zgrep analytics_collect_data var/log/support_report.log var/log/support_report.log.1.gz | tail`

a.はい – クエリからの出力がジョブの成功を示している場合（例：） `Cron Job analytics_collect_data is successfully finished` 次の手順に進みます [手順 9](#step-9).\
b. NO - ログにレコードがない場合、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
c.はい – レコードはあるがエラーがある場合は、に進みます。 [手順 10](#step-10).

+++

## 手順 9 - チェック `data.tgz` ファイル {#step-9}

+++**ファイルを実行します `data.tgz` システムに存在し、アクセスログにレコードがありますか？**

ファイルを確認するには `data.tgz` が存在する場合は、コマンドを実行します。

```
ls -ltr pub/media/analytics/<there should be a directory with hash name>/
```

access.logs にレコードがあることを確認するには、次のコマンドを実行します。

```
zgrep -i analytics /var/log/platform/[cluster_id|cluster_id_stg]/access.log* | grep MagentoBI
```

a.はい – ファイルが `data.tgz` が存在し、アクセスログにレコードがありますが、まだ 404 エラーが発生しています。次の操作が必要です [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b.いいえ – に進みます。 [手順 10](#step-10).

+++

## 手順 10 - エラーメッセージを確認 {#step-10}

+++**cron ジョブからエラーメッセージがスローされていますか。**

例： `core_config_data` エラーが表示されているテーブル *「/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0 ファイルは削除できません*. 警告！unlink （/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0?lang=en）：そのようなファイルやディレクトリはありません*

a.はい。で ACSD-50165 パッチを使用します。 [ファイルを削除できません。 警告！リンク解除：管理からのファイルまたはディレクトリのエラーがありません](/help/troubleshooting/miscellaneous/file-cannot-be-deleated-no-file-or-directory.md)、ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。\
b.いいえ – に進みます。 [手順 11](#step-11).

+++

## 手順 11 - ページビルダーエラーの確認 {#step-11}

+++**ページビルダーによってエラーが発生していますか？**

例： `report.ERROR: Cron Job analytics_collect_data has an error: substr_count() expects parameter 1 to be string, null given. Statistics: {"sum":0,"count":1,"realmem":0,"emalloc":0,"realmem_start":224919552,"emalloc_start":216398384} [] []`

a.はい。で MDVA-19391 パッチを使用します。 [Adobe Commerceの一般的な高度なレポート cron ジョブエラー](/help/troubleshooting/known-issues-patches-attached/advanced-reporting-cron-job-errors-magento-commerce.md)、ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

[手順 1 に戻る](#step-1)
