---
title: Adobe Commerceの高度なレポートのトラブルシューティング
description: Adobe Commerceの高度なレポートの問題は、このトラブルシューティングツールを使用して解決できます。 これには、データが表示されない高度なレポートや 404 エラーが含まれます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。
exl-id: 7ef9870c-b6b6-4144-a5a7-81aa20a1606c
feature: Cache, Support
role: Developer
source-git-commit: 50262a7b98091d4388668c984cfd8237bd534bad
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 0%

---

# Adobe Commerceの高度なレポートのトラブルシューティング

Adobe Commerceの高度なレポートの問題は、このトラブルシューティングツールを使用して解決できます。 これには、データが表示されない高度なレポートや 404 エラーが含まれます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。

## 手順 1 - サイトが高度なレポート要件を満たしていることを確認する {#step-1}

+++**Web サイトは高度なレポート要件を満たしていますか？**

詳細レポートを使用すると、404 エラーページが表示される。 Web サイトは [ 高度なレポート要件 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#requirements) を満たしていますか？

a.はい – [ 手順 2](#step-2) に進みます。\
b.いいえ – [ 高度なレポート要件 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#requirements) の手順に従って、サイトの高度なレポート要件を完了します。 次に [ 手順 2](#step-2) に進みます。

+++

## 手順 2 – 複数の基本通貨での注文があるか。 {#step-2}

+++**複数の基本通貨が使用されていますか？**

複数の基本通貨を（注文および設定内で）使用していますか。 [!DNL SQL] コマンドを実行して、現在の設定を取得します：`SELECT value FROM core_config_data WHERE path = 'currency/options/base';`。

a.はい。クエリで複数の行が返される場合、1 つの通貨のみをサポートしているので、**[!UICONTROL Advanced Reporting]** を使用できません。 [Adobe Commerce Intelligence](https://experienceleague.adobe.com/en/docs/commerce-business-intelligence/mbi/guide-overview) を使用する必要があります。 これを設定するには、アカウントチームにお問い合わせください。
b. NO – 出力には 1 つの通貨のみが表示されます。 例：`USD`。 複数の基本通貨が（注文で）使用されたことはありますか？ 次の [!DNL SQL] コマンドを実行して、注文の履歴データを取得します。\
`SELECT DISTINCT base_currency_code FROM sales_order;`。
**メモ：このコマンドでは、完全なテーブルスキャンが必要です。そのため、レコード数が多いテーブルの場合、クエリの実行中に履歴オーダーデータを取得するために** パフォーマンスに影響が及ぶ可能性があります。
複数の基本通貨が使用されたことがある場合は、1 つの通貨のみをサポートしているので、高度なレポートを使用できません。 出力に 1 つの通貨のみが表示される場合は、[ 手順 3](#step-3) に進みます。

+++

## 手順 3 – 分割データベースが使用中かどうかを確認する {#step-3}

+++**分割データベースソリューションを使用していますか？**

[ 分割データベースソリューション ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/split-db/multi-master) を使用していますか？

a.はい。Advanced Reporting 404 のパッチ **MDVA-26831** エラーを使用して、スプリット データベース ソリューションとキャッシュをクリアします。 ジョブが再び実行されるまで 24 時間待ってから、もう一度試してください。\
b.いいえ – [ 手順 4](#step-4) に進みます。

+++

## 手順 4 – 詳細レポートが有効であることを確認 {#step-4}

+++**詳細レポートは有効になっていますか？**

**管理者**/**ストア**/**設定**/**設定**/**一般**/**詳細レポート** をオンにします。 詳細な手順については、[ 詳細レポート：詳細レポートを有効にする ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#step-1-enable-advanced-reporting) を参照してください。

a.はい – [ 手順 5](#step-5) に進みます。\
b.いいえ – [ 詳細レポートを有効にする ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#step-1-enable-advanced-reporting) を選択して保存し、Adobe Commerceと詳細レポートが同期するまで 24 時間待ちます。 データが読み込まれるかどうかを確認します。 問題が解決した場合。 [ ステップ 5](#step-5) に進まない場合。

+++

## 手順 5 - トークンの確認 {#step-5}

+++**トークンはありますか？**

次のクエリを実行して、トークンがあることを確認します。`SELECT * FROM core_config_data WHERE path LIKE 'analytics/general/token' \G` トークンはありますか？

a.はい – [ 手順 7](#step-7) に進みます。\
b.いいえ – トークンの値が NULL であるか、データベースにレコードがない場合は、[ 手順 6](#step-6) に進みます。

+++

## 手順 6 – 行を使用 {#step-6}

+++**クエリはローを返しますか？**

次のクエリを実行して、フラグテーブルのカウンター値を確認します。``SELECT * FROM `flag` where `flag_code` = 'analytics_link_subscription_update_reverse_counter'\G`` クエリは行を返しますか？

a.はい – 次の手順を実行します。1. 次のクエリを実行します。\
``DELETE from `flag` where `flag_code` = 'analytics_link_subscription_update_reverse_counter';``\
2\. [ 設定で詳細レポートモジュールを無効にする ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#step-1-enable-advanced-reporting) 有効にする）および [ トークンを再認証 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#verify-that-the-integration-is-active) します。\
3\. Adobe Commerceと詳細レポートが同期するまで 24 時間待ちます。 詳細レポートでデータが表示されない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。\
b.いいえ – クエリから何も返されない場合は、次の手順に従います。1. [ 設定で詳細レポートモジュールを無効にする ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#step-1-enable-advanced-reporting) 有効にする）および [ トークンを再認証 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/business-intelligence#advanced-reporting#verify-that-the-integration-is-active) します。\
2\. Adobe Commerceと詳細レポートが同期するまで 24 時間待ちます。 詳細レポートでデータが表示されない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。

+++

## 手順 7 - テーブル内のレコード `cron_schedule` 確認 {#step-7}

+++**`cron_schedule` テーブルにレコードがありますか？**

次のクエリを実行して、ジョブ `analytics_collect_data` が実行されたことを確認します：`SELECT * FROM cron_schedule WHERE job_code LIKE 'analytics_collect_data' \G`

a.はい。レコードが存在し、**status** 列に _missed_ と表示されている場合は、このサポート情報記事の Update Advanced Reporting のパッチを使用して、独自の cron グループで実行します。\
b.はい – レコードが存在し、**ステータス** 列が _成功_ と表示されている場合は、[ 手順 9](#step-9) に進みます。\
c.はい – レコードが存在し、**ステータス** 列が _エラー_ になっている場合は、[ 手順 8.](#step-8) に進みます\
d.いいえ – レコードがない場合は、[ 手順 8](#step-8) に進みます。

+++

## 手順 8 - `support_report.log` でジョブを確認する {#step-8}

+++**ジョブは `support_report.log` にログインしましたか？**

次のコマンドを実行します。`zgrep analytics_collect_data var/log/support_report.log var/log/support_report.log.1.gz | tail`

a.はい – クエリからの出力がジョブの成功を示している場合（例：`Cron Job analytics_collect_data is successfully finished` は [ 手順 9](#step-9)。\
b.いいえ – ログにレコードがない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。\
c.はい – レコードが存在するにもかかわらずエラーが発生した場合は、[ 手順 10](#step-10) に進みます。

+++

## 手順 9 - `data.tgz` ファイルを確認する {#step-9}

+++**ファイル `data.tgz` はシステムに存在し、アクセスログにレコードがありますか？**

ファイル `data.tgz` が存在することを確認するには、次のコマンドを実行します。このコマンドは、ハッシュ名を持つディレクトリを返します。

```
ls -ltr pub/media/analytics/
```

access.logs にレコードがあることを確認するには、次のコマンドを実行します。

* Commerce Cloudで：

  ```
  {{zgrep -i analytics /var/log/platform/*/access.log* | grep MagentoBI}}
  ```

* オンプレミスの場合は、それに応じてファイルパスを次のように置き換えます。
  `zgrep -i analytics <your web server's log path>/access.log* | grep MagentoBI`

a.はい。ファイル `data.tgz` が存在し、アクセスログにレコードがあるが、404 エラーが解決しない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) する必要があります。\
b.いいえ – [ 手順 10](#step-10) に進みます。

+++

## 手順 10 - エラーメッセージを確認 {#step-10}

+++**cron ジョブによってエラーメッセージがスローされますか？**

例：`cron_schedule` の表に「*/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0 ファイルは削除できません* というエラーが表示されます。 警告！unlink （/app/var/tmp/analytics/tmp/.nfsb3b6041dd44588a0000850c0?lang=en）：そのようなファイルやディレクトリはありません*

a.はい – ACSD-50165 パッチを使用してください [ ファイルは削除できません。 警告！unlink：管理 ](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26887) にファイルまたはディレクトリのエラーがありません。ジョブが再実行されるまで 24 時間待ってから、再試行してください。\
b.いいえ – [ 手順 11](#step-11) に進みます。

+++

## 手順 11 - ページビルダーエラーの確認 {#step-11}

+++**ページビルダーが原因でエラーが発生していますか？**

例：`report.ERROR: Cron Job analytics_collect_data has an error: substr_count() expects parameter 1 to be string, null given. Statistics: {"sum":0,"count":1,"realmem":0,"emalloc":0,"realmem_start":224919552,"emalloc_start":216398384} [] []`

回答：はい。Adobe Commerceの一般的な詳細レポートの cron ジョブエラーで MDVA-19391 パッチを使用し、ジョブが実行されるまで 24 時間待ってから、もう一度試してください。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

[手順 1 に戻る](#step-1)

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
