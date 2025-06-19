---
title: Adobe Commerceのデータベースストレージに関するトラブルシューティング
description: この記事は、データベースに関する問題が発生したAdobe Commerceのお客様向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状と構成に応じて、データベースの領域と構成に関する問題のトラブルシューティング方法を示します。
exl-id: f7b09023-7129-4fd0-9bb5-02a2228bc148
feature: Observability, Services, Storage, Support
role: Developer
source-git-commit: 129e24366aedb132adb84e1f0196d2536422180f
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# Adobe Commerceのデータベースストレージに関するトラブルシューティング

この記事は、データベースに関する問題が発生したAdobe Commerceのお客様向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状と構成に応じて、データベースの領域と構成に関する問題のトラブルシューティング方法を示します。

## 手順 1 - スペースの問題があるディレクトリの特定 {#step-1}

+++**スペースの不足によって発生する `/tmp` しい問題はありますか？**

これは、`/tmp` マウントが満杯、サイトダウン、ノードに SSH 接続できないなど、様々な症状で示される可能性があります。 また、「デバイスに空き容量がありません _（28）_ などのエラーが発生している可能性があります。 `/tmp` がいっぱいになったことによるエラーのリストについては、[/tmp mount full](/help/troubleshooting/miscellaneous/tmp-mount-full.md) を参照してください。

または、スペースの不足が原因で `/data/mysql` の問題が発生していますか？ これは、サイトの停止、買い物かごに製品を追加できない、データベースへの接続に失敗した、_SQLSTATE\[08S01\]: Communication link failure: 1047 WSREP_ のような Galeria エラーなど、さまざまな現象でも示されます。 [!DNL MySQL] ディスク領域の不足によるエラーのリストについては、[[!DNL MySQL]  クラウドインフラストラクチャ上のAdobe Commerceのディスク領域が少ない ](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) を参照してください。

ディスク容量に関する問題が発生しているかどうか、およびNew Relic アカウントがあるかどうかが不明な場合は、[New Relic Infrastructure monitoring Hosts ページ ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/) にアクセスしてください。 そこから、[**ストレージ**] タブをクリックし、[**グラフの表示**] ドロップダウン・リストを 5 から 20 に変更して、[ ディスク使用率 %] グラフまたはテーブルでディスクの使用率が高いかどうかを確認します。 詳しい手順については、[New Relic インフラストラクチャの監視/「ストレージ」タブ ]https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#storage）を参照してください。

上記の現象が発生した場合は、inode の状態を調べて、ファイル番号の問題が原因でないことを確認してください。 これを行うには、CLI/ターミナルで次のコマンドを実行します。\
`df -ih`

IUse% は 90% を超えていますか。

a.はい。これは、ファイルが多すぎることが原因です。 [ クラウドインフラストラクチャー上のAdobe Commerceのディスク容量不足の場合に、ファイルを安全に削除する手順 ](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26889) を確認します。 これらの手順を完了したら [ 手順 2](#step-2) に進みます。 さらに多くのスペースをリクエストする場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。\
b. NO - スペースを確認します。 `df -h | grep mysql` を実行し、CLI/ターミナルで `df -h | grep tmp` を実行して、`/tmp` ディレクトリと `/data/mysql` ディレクトリのディスク容量の使用状況を確認します。 [ 手順 3](#step-3) に進みます。

+++

## 手順 2 - ディスク容量の確認 {#step-2}

+++**ディスク領域の使用状況を確認しますか？**

ファイルの数を減らしたら、`df -h | grep mysql` を実行し、CLI/ターミナルで `df -h | grep tmp` を実行して、`/tmp` と `/data/mysql` のディスク・スペースの使用状況を確認します。 70% を超える値が `/tmp` または `/data/mysql` に使用されていますか？

a.はい – [ 手順 3](#step-3) に進みます。
b. NO - クエリによって使用可能なストレージが使い果たされる可能性があります。 これにより、ノードがクラッシュして、クエリが強制終了し、`tmp` ファイルが削除される可能性があります。 [!DNL MySQL] CLI の `SHOW PROCESSLIST;` の出力を調べて、問題の原因となっている可能性のあるクエリを探します。 [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) すると、空き容量を増やすことが必要になります。

+++

## 手順 3 – 使用率の高いディレクトリの特定 {#step-3}

+++**70% を超える値が使用されているディレクトリはどれですか？**

70% を超える使用率を持つディレクトリはどれですか。 `/tmp` か `/data/mysql` か？

>[!NOTE]
>
>デフォルトでは、データベース tmpdir は `/tmp` に書き込みます。 データベース構成がこのデフォルトのままであることを確認するには、[!DNL MySQL] CLI で次のコマンドを実行します。`SHOW VARIABLES LIKE "TMPDIR";` データベース tmpdir がまだ `/tmp` に書き込み中の場合は、Value 列に `/tmp` が表示されます。

a. `/tmp` - [ 手順 4](#step-4) に進みます。 \
b. `/data/mysql` - [ 手順 5](#step-5) に進みます。

+++

## 手順 4 - /tmp mount full のトラブルシューティング {#step-4}

+++**/tmp mount full のトラブルシューティング**

[Adobe Commerceの/tmp mount full のトラブルシューティング ](/help/troubleshooting/miscellaneous/tmp-mount-full.md)、記事を下にスクロールして、ソリューションとベストプラクティスを試します。 次に、`df -h | grep mysql` を実行し、CLI/ターミナルで `df -h | grep tmp` を実行して、`/tmp` ディレクトリと `/data/mysql` ディレクトリのディスク容量の使用状況を確認します\
  70% 未満を使用していますか？

>[!NOTE]
>
>[Adobe Commerceの/tmp mount full のトラブルシューティング ](/help/troubleshooting/miscellaneous/tmp-mount-full.md) のソリューションは、データベース tmpdir の変数を変更していないマーチャント向けに設計されています。この変数は、デフォルトでは `/tmp` に書き込まれます。 tmpdir の値を変更した場合、「[Adobe Commerceの/tmp mount full のトラブルシューティング ](/help/troubleshooting/miscellaneous/tmp-mount-full.md) の手順は役に立ちません。

回答：はい、問題は解決しました。 \
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、空き容量を増やします。

+++

## 手順 5 - デフォルトを確認 {#step-5}

+++**デフォルトをオン**

データベースの設定が元のデフォルトの状態でなくなる場合があります。 [!DNL MySQL] CLI: `SELECT @@DATADIR;` でを実行して、データベースの tmpdir 設定を見つけます。 `/data/mysql/` が出力された場合、データベース tmpdir は `/data/mysql/` に書き込み中です。 [[!DNL MySQL]  クラウドインフラストラクチャ上のAdobe Commerceのディスク容量が少なくなっています ](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md) の手順に従って、このディレクトリの容量を増やしてみてください。 次に、`df -h | grep mysql` を実行し、CLI/ターミナルで `df -h | grep tmp` を実行して、`/data/mysql` と `/tmp` でディスク容量の使用状況を確認します。\
  70% 未満を使用していますか？

回答：はい、問題は解決しました。 \
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、空き容量を増やします。

+++

[ 手順 1 に戻る ](#step-1)

## 関連資料

* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
