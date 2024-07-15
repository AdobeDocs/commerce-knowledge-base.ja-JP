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

データを同期するには、ソース環境から手動でデータベースをダンプする必要があります。 別の環境にデータを転送するには、その後、ソースダンプをターゲット環境にアップロードして読み込む必要があります。 詳しくは、開発者向けドキュメントの [Adobe Commerce コードのクラウドプロジェクトへのインポート/Adobe Commerce データベースのインポート ](https://devdocs.magento.com/cloud/setup/first-time-setup-import-import.html) を参照してください。

クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの場合は、ステージング環境と実稼動環境から統合マスターブランチに同期することもできます。 この同期では、コードの取り込みとプッシュのみが行われ、データはプッシュされません。 データを同期するには、データベースデータをダンプし、別の環境のデータベースにプッシュする必要があります。

>[!WARNING]
>
>ステージング環境および実稼動環境のクラスターでは、データベースの同期を実行できません。

## ある環境から別の環境にファイルを同期するには

ある環境から別の環境にファイルを同期するには、`rsync` コマンドを使用します。 詳しくは、開発者向けドキュメントの [ コードのデプロイと静的ファイルおよびデータの移行/rsync を使用したファイルの移行 ](https://devdocs.magento.com/cloud/live/stage-prod-migrate.html#migrate-files-using-rsync) を参照してください。

>[!NOTE]
>
>コードを統合からステージングに同期する場合は、統合ブランチから実行する必要があります。 手順については、開発者向けドキュメントの [ 環境の親からの同期 ](/docs/commerce-cloud-service/user-guide/project/console-branches.html#sync-an-environment) を参照してください。
