---
title: データとファイルを実稼動環境からステージング環境またはステージング環境から統合環境に同期
description: この記事では、実稼動環境をクラウドインフラストラクチャ上のAdobe Commerceのステージングに同期する方法について説明します。同期は不可能です。
exl-id: e3d001d1-1b2a-41b5-9b4a-00e53dc9d001
feature: Integration, Build
source-git-commit: ef294ddc9c4a12b06ce7738cb4702253dd892f3b
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# データとファイルを実稼動環境からステージング環境またはステージング環境から統合環境に同期

Adobe Commerceこの記事では、クラウドインフラストラクチャー上で実稼動環境をステージング環境に同期させる方法について説明します。ユーザーインターフェイスまたはMagentoクラウド CLI を使用して同期することはできません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.x、2.4.x

## ある環境から別の環境にデータを同期するには

データを同期するには、ソース環境から手動でデータベースをダンプする必要があります。 別の環境にデータを転送するには、その後、ソースダンプをターゲット環境にアップロードして読み込む必要があります。 詳しくは、を参照してください [Adobe Commerce コードをクラウドプロジェクトに読み込む/Adobe Commerce データベースを読み込む](https://devdocs.magento.com/cloud/setup/first-time-setup-import-import.html) 開発者向けドキュメントを参照してください。

クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの場合は、ステージング環境と実稼動環境から統合マスターブランチに同期することもできます。 この同期では、コードの取り込みとプッシュのみが行われ、データはプッシュされません。 データを同期するには、データベースデータをダンプし、別の環境のデータベースにプッシュする必要があります。

>[!WARNING]
>
>ステージング環境および実稼動環境のクラスターでは、データベースの同期を実行できません。

## ある環境から別の環境にファイルを同期するには

環境間でファイルを同期するには、を使用します `rsync` コマンド。 詳しくは、を参照してください [コードのデプロイと静的ファイルとデータの移行/rsync を使用したファイルの移行](https://devdocs.magento.com/cloud/live/stage-prod-migrate.html#migrate-files-using-rsync) 開発者向けドキュメントを参照してください。

>[!NOTE]
>
>コードを統合からステージングに同期する場合は、統合ブランチから実行する必要があります。 手順については、を参照してください [環境の親から同期](/docs/commerce-cloud-service/user-guide/project/console-branches.html#sync-an-environment) 開発者向けドキュメントを参照してください。
