---
title: クラウドインフラストラクチャー上のAdobe Commerceで環境をリセット
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境をロールバックする様々なシナリオについて説明します。
exl-id: e6b27838-ca1e-415f-a098-2aa2576e3f20
feature: Best Practices, Build, Cloud, Console
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceで環境をリセット

この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境をロールバックする様々なシナリオについて説明します。

お客様の状況に最も適したものを選択してください。

* 計画アクティビティ（計画デプロイメントまたはアップグレード）がある場合 – [ シナリオ 1：計画アクティビティ） ](#scen1)。
* 有効なスナップショットがある場合 – [ シナリオ 2：スナップショットの復元 ](#scen2)。
* 安定したビルドで、有効なスナップショットがない場合 – [ シナリオ 3：スナップショットがない、安定したビルド（SSH 接続が使用可能） ](#scen3)。
* ビルドが中断され、有効なスナップショットがない場合 – [ シナリオ 4：スナップショットなし、ビルドが中断（SSH 接続なし） ](#scen4)。

## シナリオ 1：計画アクティビティ

展開またはアップグレードを計画している場合、準備の一環として、販売者が次の作業を行う [!UICONTROL Rollback] が最も簡単で推奨されます。

>[!NOTE]
>
>常にこれらの手順を最初に **[!UICONTROL Staging Environment]** でテストします。

<u> アップグレード/デプロイメントアクティビティの 5 日前 </u>:

1. 現在のデータベースのサイズを確認します。
1. [!UICONTROL Database Dump] を保持するのに十分なディスク容量が `/data/exports` にあることを確認します。 十分なディスク領域がない場合は、不要なデータを削除するか、サポートケースを作成してディスクの拡張をリクエストします。

<u> 変更日 </u>:

1. Web サイトを [!UICONTROL Maintenance Mode] に配置します。
[ ユーザーガイドで [!UICONTROL Maintenance Mode]](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html) を有効または無効にする」および「アップグレードのオプションを [[!UICONTROL Maintenance Mode] 定する ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/troubleshooting/maintenance-mode-options.html) について詳しくは、アップグレードガイドを参照してください。
1. cron ジョブを無効にします。 Cron ジョブの無効化について詳しくは、[cron プロパティガイド ](<https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property#disable-cron-jobs>) を参照してください。
1. 地元の [[!UICONTROL Database Dump]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html) を取る。

<u>[!UICONTROL Rollback] が必要な場合 </u>:

1. [!DNL MariaDB] などのアプリケーションがこの計画されたアクティビティの一部としてアップグレードされた場合は、まず、そのアプリケーションを以前のバージョンに再インストールしてください。
1. ローカル [!UICONTROL Database Dump] を使用してデータベースを [!UICONTROL Rollback] び出し、[!DNL MariaDB] にインポートします。
1. [!DNL Git] を介してコードを以前の作業用バージョンに [!UICONTROL Rollback] きます。

[!UICONTROL Snapshots] の使用は、**[!UICONTROL Rollback] ークフローが必要な場合** セクションの手順 2 で前述したように、ローカルア [!UICONTROL Database Dump] ットと比較してデータを取得するのに非常に時間がかかるので、アップグレードや予定アクティビティの [!UICONTROL rollbacks/restores] ークフローには推奨されません。

ノード/サーバ上に保持されるわけでは [!UICONTROL Snapshots] く、別のストレージ・ブロックに保持されるため、そのデータはネットワークを介してブロック・ストレージから新しいディスクに送信される必要があるため、処理に時間がかかります。 その後、新しいディスクがノードにマウントされ、ノードまたはサーバーに接続されている元のディスクに取得/読み込みの準備が整います。

これをローカル [!UICONTROL Database Dump] ータの読み込みと比較すると、データはノード/サーバー上で既に取得可能なので、[!UICONTROL Database Import] ータのみが必要なので、多くの時間が節約されます。

## シナリオ 2：スナップショットの復元

開発者向けドキュメントの [ クラウドインフラストラクチャー上のAdobe Commerceのスナップショットを復元する ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots#restore-snapshot) をお読みください。

>[!NOTE]
>
>スナップショットの作成は、クラウドインフラストラクチャアカウントでAdobe Commerceにアクセスした後、大規模な変更を適用する前の最初の手順である必要があります。 これはベストプラクティスであり、強く推奨されます。

開発者向けドキュメントの [ スナップショットの作成 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots#create-snapshot) をお読みください。

## シナリオ 3：スナップショットがない、安定して構築（SSH 接続を使用可能）

このセクションでは、スナップショットを作成していないが、SSH 経由で環境にアクセスできる場合に環境をリセットする方法を示します。

手順は次のとおりです。

1. 構成管理を無効にします。
1. Adobe Commerce ソフトウェアをアンインストールします。
1. [!DNL git] ブランチをリセットします。

これらの手順を実行した後：

* Adobe Commerceのインストールがバニラ状態に戻ります（データベースが復元され、デプロイメント設定が削除され、ディレクトリ `var` 消去されます）。
* [!DNL git] ブランチが、過去に目的の状態にリセットされます。

以下の詳細な手順をお読みください。

### 手順 0 （前提条件）:config.php を削除して、構成管理を無効にします

デプロイメント中に以前の設定が自動的に適用されないように、設定管理を無効にする必要があります。

構成管理を無効にするには、`/app/etc/` ディレクトリに `config.php` ファイルが含まれていないことを確認してください。

設定ファイルを削除するには、次の手順に従います。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 設定ファイル `rm app/etc/config.php` を削除します。

詳しくは、設定管理を参照してください。

* [ クラウドインフラストラクチャ上のAdobe Commerceでのデプロイメントのダウンタイムを短縮する ](/help/how-to/general/magento-cloud-reduce-deployment-downtime-with-configuration-management.md) については、サポートナレッジベースを参照してください。
* 開発者向けドキュメントの [ ストア設定の設定管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html) を参照してください。

### 手順 1:setup:uninstall コマンドを使用してAdobe Commerce ソフトウェアをアンインストールする


Adobe Commerce ソフトウェアをアンインストールすると、データベースが削除されて復元され、配置設定が削除されて、`var` の下のディレクトリがクリアされます。

開発者向けドキュメントの [Adobe Commerce ソフトウェアをアンインストールする ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall.html) をお読みください。

Adobe Commerce ソフトウェアをアンインストールするには、次の手順に従います。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 実行 `setup:uninstall`:`bin/magento setup:uninstall`
1. アンインストールを確認します。

次のメッセージが表示され、アンインストールが正常に完了したことを確認します。

```php
[SUCCESS]: Magento uninstallation complete.
```

つまり、Adobe Commerce（DB を含む）のインストールが本物の（Vanilla）状態に戻りました。

### 手順 2:[!DNL git] ブランチのリセット

リセット [!DNL git] ると、コードが以前に目的の状態に戻ります。

1. ローカル開発環境に環境のクローンを作成します。 Cloud Console で次のコマンドをコピーできます。    ![copy_git_clone.png](assets/copy_git_clone.png)
1. コミット履歴にアクセスします。 `--reverse` を使用して履歴を逆の順序で表示すると、より便利です：`git log --reverse`
1. 正常に動作しているコミットハッシュを選択します。 コードを本物の状態（Vanilla）にリセットするには、ブランチ（環境）を作成した最初のコミットを見つけます。
   ![ 代替テキスト ](image.png)
1. ハード [!DNL git] リセットの適用：`git reset --h <commit_hash>`
1. 変更をサーバーにプッシュ：`git push --force <origin> <branch>`

これらの手順を実行すると、[!DNL git] ブランチがリセットされ、[!DNL git] の変更ログ全体がクリアされます。 最後の [!DNL git] プッシュトリガーは、すべての変更を適用してAdobe Commerceを再インストールするために再デプロイすることです。

## シナリオ 4：スナップショットなし、ビルドが中断（[!DNL SSH] 接続なし）

ここでは、クリティカル状態の環境をリセットする方法について説明します。デプロイメントプロシージャでは正常に動作するアプリケーションを構築できないため、[!DNL SSH] 接続が使用できなくなります。

このシナリオでは、まず [!DNL git] リセットを使用してAdobe Commerce アプリケーションの動作ステータスを復元し、次にAdobe Commerce ソフトウェアをアンインストールします（データベースを削除して復元するには、デプロイメント設定を削除する必要があります）。 シナリオにはシナリオ 3 と同じステップが含まれますが、ステップの順序は異なり、追加のステップとして再デプロイが強制されます。 手順は次のとおりです。

1. [分岐をリセ  [!DNL git]  トします。](/help/how-to/general/reset-environment-on-cloud.md#reset-git-branch)
1. [構成管理を無効にします。](/help/how-to/general/reset-environment-on-cloud.md#disable_config_management)
1. [Adobe Commerce ソフトウェアをアンインストールします。](/help/how-to/general/reset-environment-on-cloud.md#setup-uninstall)
1. 再デプロイを強制的に実行します。

これらの手順を実行すると、シナリオ 3 と同じ結果が得られます。

### 手順 4：再デプロイの強制

コミットを作成し（これは空のコミットである可能性がありますが、お勧めしません）、トリガーにプッシュして再デプロイします。

```git
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## setup:uninstall が失敗した場合は、データベースを手動でリセットします

`setup:uninstall` コマンドの実行がエラーで失敗し、完了しない場合は、次の手順で DB を手動でクリアできます。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. MySQL DB: `mysql -h database.internal` に接続します（Pro 環境の場合は [MySQL サービスの設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/mysql.html) を参照してください）。
1. `main` DB : `drop database main;` をドロップします。
1. 空の `main` DB を作成します：`create database main;`
1. 次の設定ファイルを削除します：`config.php`、`config.php.bak`、`env.php`、`env.php.bak`

DB をリセットした後 [ 環境に  [!DNL git]  プッシュしてトリガーを再デプロイし ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/examples/example-using-cli.html) 新しく作成した DB にAdobe Commerceをインストールします。 または [redeploy コマンドを実行します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html#environment-commands)。
