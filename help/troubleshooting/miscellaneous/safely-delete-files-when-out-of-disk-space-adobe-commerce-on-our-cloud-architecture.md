---
title: クラウドインフラストラクチャー上のAdobe Commerceでディスクの容量が不足した場合に、ファイルを安全に削除できます
description: この記事では、ディスク容量が不足し、ファイルを安全に削除する必要がある場合の解決策を説明します。 このアクションを検討する前に、開発者向けドキュメントの [ ディスク容量の管理 ] （https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space#no-space-left）を確認してください。 その記事の手順が自分に適していない場合や問題が解決しない場合は、この記事の手順を確認してください。
exl-id: 6b0a5c1a-8db4-49d7-a785-b4e0bbaea0df
feature: Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceでディスクの容量が不足した場合に、ファイルを安全に削除できます

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.4.2 - 2.4.7
* これは、専用の Pro クラスターに固有のものです。 スターター環境と統合環境は単一ノードで、`/data/exports` ディレクトリはありません。

## ディスク容量の不足の兆候

ディスク容量が不足していると、デプロイメントが停止したり、ディスク容量超過の警告が表示されたり、パフォーマンスが低下したりする可能性があります。
ファイルシステムが使用しているディスク容量を確認するには、CLI/ターミナルで次のコマンドを実行します。

`df -h`


## ファイルを安全に削除してディスク容量を増やす方法

ファイルは、アプリケーションのマウントポイント、`/app` パスまたは `/mnt/shared` 経由から削除できます。 同じファイルにアクセスする方法は 2 つあります。

>[!WARNING]
>
>**`/data/exports`** ージのコンテンツを変更または削除しないでください。
>
>`/data/exports` は共有ファイルシステムの基盤となるストレージであり、GlusterFS によって管理されます。
>
>このファイル・システムには、ファイルの内容だけでなく、ファイル・システムの状態に関するメタデータも含まれており、クラスタのノード間の同期を可能にします。 **このファイル・システム内で直接ファイルを変更または削除すると、shared >filesystem が破損し、大規模な修復またはデータ・リカバリが必要になります。**

クリアの対象となる可能性のある最大のファイルを見つけるには、次のコマンドを実行します（大規模なプロジェクトやビジー状態のプロジェクトでは最大 1 時間かかる場合があります）。

```bash
FS='/data/exports';NUMRESULTS=20;resize;clear; echo "Please find below the Largest Directories and Files:";date;df -h $FS; echo "Largest Directories:";nice -n 19 find /app/*/ -type d -ls 2>/dev/null| sort -rnk1| head -n $NUMRESULTS| awk '
{printf "%d MB %s\n", $1/1024,$2}
';echo "Largest Files:"; nice -n 19 find /app/*/ -type f -ls 2>/dev/null| sort -rnk7| head -n $NUMRESULTS|awk '
{printf "%d MB\t%s\n", ($7/1024)/1024,$NF}
'; echo "Please use the above information to clear any unwanted data from the server, it is important this is done as soon as possible to ensure your server stays functional.";
```

コマンドの出力には、指定されたサイズで最大のファイルとディレクトリのリストが含まれます。

## 関連資料

サポートナレッジベースでは、

* [クラウド上の統合環境のディスク容量を増やす](/help/how-to/general/increase-disk-space-for-integration-environment-on-cloud.md)
* [ディスク容量が少ない](/help/troubleshooting/miscellaneous/low-disk-space.md)

開発者向けドキュメントでは、

* [ ディスク容量の管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space)
