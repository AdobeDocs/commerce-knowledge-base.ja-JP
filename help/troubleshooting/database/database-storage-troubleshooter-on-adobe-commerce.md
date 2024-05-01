---
title: Adobe Commerceのデータベースストレージに関するトラブルシューティング
description: この記事は、データベースに関する問題が発生したAdobe Commerceのお客様向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状と構成に応じて、データベースの領域と構成に関する問題のトラブルシューティング方法を示します。
exl-id: f7b09023-7129-4fd0-9bb5-02a2228bc148
feature: Observability, Services, Storage, Support
role: Developer
source-git-commit: 324cce66df1e4ab7ec4ef8fb6512c3acbabdf3ab
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Adobe Commerceのデータベースストレージに関するトラブルシューティング

この記事は、データベースに関する問題が発生したAdobe Commerceのお客様向けのトラブルシューティングツールです。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。 症状と構成に応じて、データベースの領域と構成に関する問題のトラブルシューティング方法を示します。

## 手順 1 - スペースの問題があるディレクトリの特定 {#step-1}

+++**持っていますか。 `/tmp` スペースの不足によって発生する問題**

これは、次のような様々な症状で示されます `/tmp` マウントがフルであるか、サイトがダウンしているか、ノードに SSH 接続できない。 次のようなエラーが発生している場合もあります。 _デバイスにスペースが残っていません（28）_. から生じるエラーのリストの場合 `/tmp` フルである、確認する [/tmp mount full](/help/troubleshooting/miscellaneous/tmp-mount-full.md).

または、 `/data/mysql` スペースの不足によって発生する問題 これは、サイトの停止、顧客が買い物かごに製品を追加できない、データベースへの接続に失敗した、Galeria の次のようなエラーなど、様々な症状でも示されます _SQLSTATE\[08S01\]：通信リンク エラー：1047 WSREP_. MySQL のディスク容量不足によるエラーのリストについては、を参照してください。 [クラウドインフラストラクチャー上のAdobe Commerceで MySQL のディスク領域が不足している](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md).

ディスク容量に関する問題が発生しているかどうか、およびNew Relic アカウントをお持ちの場合は、 [「New Relic インフラストラクチャ監視ホスト」ページ](https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/). そこから、 **ストレージ** タブで、 **グラフ表示** 5～20 の結果をドロップダウンし、[Disk Used %] グラフまたは表でディスクの使用率が高いかどうかを表で確認します。 詳細な手順については、次を参照してください [New Relic インフラストラクチャの監視/「ストレージ」タブ]https://docs.newrelic.com/docs/infrastructure/infrastructure-ui-pages/infra-hosts-ui-page/#storage）に設定します。

上記の現象が発生した場合は、inode の状態を調べて、ファイル番号の問題が原因でないことを確認してください。 これを行うには、CLI/ターミナルで次のコマンドを実行します。\
`df -ih`

IUse% は 90% を超えていますか。

a.はい。これは、ファイルが多すぎることが原因です。 でファイルを安全に削除する手順を確認します。 [クラウドインフラストラクチャー上のAdobe Commerceのディスク容量不足に対してファイルを安全に削除](/help/troubleshooting/miscellaneous/safely-delete-files-when-out-of-disk-space-adobe-commerce-on-our-cloud-architecture.md). 次の手順に進みます。 [手順 2](#step-2) これらの手順を完了したら、 さらに容量を要求する場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b. NO - スペースを確認します。 実行 `df -h | grep mysql` その後 `df -h | grep tmp` CLI/ターミナルでを使用して、でのディスク容量の使用状況を確認します。 `/tmp` および `/data/mysql` ディレクトリ。 次の手順に進みます。 [手順 3](#step-3).

+++

## 手順 2 - ディスク容量の確認 {#step-2}

+++**ディスク領域の使用状況を確認しますか？**

ファイルの数を減らしたら、を実行します。 `df -h | grep mysql` その後 `df -h | grep tmp` CLI/ターミナルで、のディスク容量の使用状況を確認します。 `/tmp` および `/data/mysql`. 次に対して 70% を超えて使用 `/tmp` または `/data/mysql`?

a.はい – に進みます。 [手順 3](#step-3).
b. NO - クエリによって使用可能なストレージが使い果たされる可能性があります。 これにより、ノードがクラッシュして、クエリが強制終了し、 `tmp` ファイル。 の出力を確認します `SHOW PROCESSLIST;` MySQL CLI で、問題の原因となっている可能性のあるクエリを検索します。 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)、より多くのスペースを要求しています。

+++

## 手順 3 – 使用率の高いディレクトリの特定 {#step-3}

+++**70% を超える使用率を持つディレクトリはどれですか。**

70% を超える使用率を持つディレクトリはどれですか。 `/tmp` または `/data/mysql`?

>[!NOTE]
>
>デフォルトでは、データベース tmpdir は以下に書き込みます。 `/tmp`. データベース設定がこのデフォルトのままであることを確認するには、MySQL CLI で次のコマンドを実行します。 `SHOW VARIABLES LIKE "TMPDIR";` データベース tmpdir がまだ書き込み中の場合 `/tmp`表示されます `/tmp` 「値」列に値を入力します。

a. `/tmp`  – に進みます。 [手順 4](#step-4). \
b. `/data/mysql`  – に進みます。 [手順 5](#step-5).

+++

## 手順 4 - /tmp mount full のトラブルシューティング {#step-4}

+++**/tmp mount full のトラブルシューティング**

[Adobe Commerceの/tmp mount full のトラブルシューティング](/help/troubleshooting/miscellaneous/tmp-mount-full.md)の場合は、記事を下にスクロールしてソリューションとベストプラクティスを試してみてください。 次を実行 `df -h | grep mysql` その後 `df -h | grep tmp` CLI/ターミナルで、のディスク容量の使用状況を確認します。 `/tmp` および `/data/mysql` ディレクトリ\
  70% 未満を使用していますか？

>[!NOTE]
>
>のソリューション [Adobe Commerceの/tmp mount full のトラブルシューティング](/help/troubleshooting/miscellaneous/tmp-mount-full.md) は、データベース tmpdir の変数を変更していないマーチャント向けに設計されています。デフォルトでは、この変数は次の場所に書き込まれます。 `/tmp`. tmpdir の値を変更した場合は、次の手順に従います。 [Adobe Commerceの/tmp mount full のトラブルシューティング](/help/troubleshooting/miscellaneous/tmp-mount-full.md) 役に立ちません。

回答：はい、問題は解決しました。 \
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)、より多くのスペースを要求しています。

+++

## 手順 5 - デフォルトを確認 {#step-5}

+++**デフォルトをオン**

データベースの設定が元のデフォルトの状態でなくなる場合があります。 MySQL CLI でを実行して、データベース tmpdir 設定を見つけます。 `SELECT @@DATADIR;`. 次の場合 `/data/mysql/` が出力され、データベース tmpdir が書き込み中である `/data/mysql/`. 次の手順に従って、このディレクトリの容量を増やしてみてください。 [クラウドインフラストラクチャ上のAdobe Commerceで、MySQL のディスク容量が少ない](/help/troubleshooting/database/mysql-disk-space-is-low-on-magento-commerce-cloud.md). 次を実行 `df -h | grep mysql` その後 `df -h | grep tmp` CLI/ターミナルで、のディスク容量の使用状況を確認します。 `/data/mysql` および `/tmp`.\
  70% 未満を使用していますか？

回答：はい、問題は解決しました。 \
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)、より多くのスペースを要求しています。

+++

[手順 1 に戻る](#step-1)
