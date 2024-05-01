---
title: クラウドインフラストラクチャー上のAdobe Commerceで環境をリセット
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境をロールバックする様々なシナリオについて説明します。
exl-id: e6b27838-ca1e-415f-a098-2aa2576e3f20
feature: Best Practices, Build, Cloud, Console
source-git-commit: ddde2385f1d94194b34e9ed51f6cbda55c916d90
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceで環境をリセット

この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境をロールバックする様々なシナリオについて説明します。

お客様の状況に最も適したものを選択してください。

* アクティビティ（導入またはアップグレードを計画）を計画している場合： [シナリオ 1：計画アクティビティ）](#scen1).
* 有効なスナップショットがある場合 –  [シナリオ 2：スナップショットの復元](#scen2).
* 安定したビルドがあるが、有効なスナップショットがない場合 –  [シナリオ 3：スナップショットがない、安定して構築（SSH 接続を使用可能）](#scen3).
* ビルドが破損しており、有効なスナップショットがない場合 –  [シナリオ 4：スナップショットなし、ビルドに障害あり（SSH 接続なし）](#scen4).

## シナリオ 1：計画アクティビティ

計画されたデプロイメントやアップグレードでは、最も簡単で推奨されます [!UICONTROL Rollback] 商人は、準備の一環として、次の操作を行います。

>[!NOTE]
>
>必ず以下の手順をテストしてください **[!UICONTROL Staging Environment]** 最初！

<u>アップグレード/デプロイメントアクティビティの 5 日前</u>:

1. 現在のデータベースのサイズを確認します。
1. 十分なディスク容量があることを確認します。 `/data/exports` 手を握る [!UICONTROL Database Dump]. 十分なディスク領域がない場合は、不要なデータを削除するか、サポートケースを作成してディスクの拡張をリクエストします。

<u>変更の日</u>:

1. Web サイトの配置先 [!UICONTROL Maintenance Mode].<br>
詳細を読む： [有効または無効 [!UICONTROL Maintenance Mode]](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html) ユーザーガイドで、 [[!UICONTROL Maintenance Mode] アップグレードのオプション](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/troubleshooting/maintenance-mode-options.html) アップグレードガイドをご覧ください。
1. ローカルを取る [[!UICONTROL Database Dump]](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html).

<u>If a [!UICONTROL Rollback] は必須です</u>:

1. 次のようなアプリケーションの場合： [!DNL MariaDB] は、この計画されたアクティビティの一環としてアップグレードされました。最初に、そのアプリケーションを以前のバージョンに再インストールしてください。
1. [!UICONTROL Rollback] ローカルを使用したデータベース [!UICONTROL Database Dump]を作成し、再度に読み込みます。 [!DNL MariaDB].
1. [!UICONTROL Rollback] 経由のコード [!DNL Git] を以前の作業バージョンに変更します。

使用 [!UICONTROL Snapshots] アップグレード/予定アクティビティには推奨されない方法です [!UICONTROL rollbacks/restores]（データの取得にローカルと比較して時間がかかるため） [!UICONTROL Database Dump]（上記の手順 2 の） **If a [!UICONTROL Rollback] は必須です** セクション。

[!UICONTROL Snapshots] ノード/サーバに保持されず、別のストレージ・ブロックに保持されます。このデータは、ネットワークを介してブロック・ストレージから新しいディスクに送信する必要があるため、処理に時間がかかります。 その後、新しいディスクがノードにマウントされ、ノードまたはサーバーに接続されている元のディスクに取得/読み込みの準備が整います。

これをローカルの読み込みと比較する場合 [!UICONTROL Database Dump]を指定すると、データはノードまたはサーバー上で既に取得可能なので、多くの時間は [!UICONTROL Database Import] は必須です。

## シナリオ 2：スナップショットの復元

読み取り： [クラウドインフラストラクチャー上のAdobe Commerceでスナップショットを復元](https://devdocs.magento.com/cloud/project/project-webint-snap.html#restore-snapshot) 開発者向けドキュメントを参照してください。

>[!NOTE]
>
>スナップショットの作成は、クラウドインフラストラクチャアカウントでAdobe Commerceにアクセスした後、大規模な変更を適用する前の最初の手順である必要があります。 これはベストプラクティスであり、強く推奨されます。

読み取り： [スナップショットの作成](https://devdocs.magento.com/cloud/project/project-webint-snap.html#create-snapshot) 開発者向けドキュメントを参照してください。

## シナリオ 3：スナップショットがない、安定して構築（SSH 接続を使用可能）

このセクションでは、スナップショットを作成していないが、SSH 経由で環境にアクセスできる場合に環境をリセットする方法を示します。

手順は次のとおりです。

1. 構成管理を無効にします。
1. Adobe Commerce ソフトウェアをアンインストールします。
1. をリセット [!DNL git] 分岐。

これらの手順を実行した後：

* Adobe Commerceのインストールがバニラ状態に戻ります（データベースが復元されました。デプロイメント設定が削除されました。次のディレクトリにあります `var` クリア）。
* あなたの [!DNL git] 過去に分岐が目的の状態にリセットされます。

以下の詳細な手順をお読みください。

### 手順 0 （前提条件）:config.php を削除して、構成管理を無効にします

デプロイメント中に以前の設定が自動的に適用されないように、設定管理を無効にする必要があります。

設定管理を無効にするには、 `/app/etc/` ディレクトリにが含まれていない `config.php` ファイル。

設定ファイルを削除するには、次の手順に従います。

1. [環境に SSH で接続する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html).
1. 設定ファイルを削除します。 `rm app/etc/config.php`

詳しくは、設定管理を参照してください。

* [クラウドインフラストラクチャ上のAdobe Commerceでのデプロイメントのダウンタイムを短縮](/help/how-to/general/magento-cloud-reduce-deployment-downtime-with-configuration-management.md) サポートナレッジベースで。
* [ストア設定の設定管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html) 開発者向けドキュメントを参照してください。

### 手順 1:setup:uninstall コマンドを使用してAdobe Commerce ソフトウェアをアンインストールする


Adobe Commerce ソフトウェアをアンインストールすると、データベースが削除されて復元され、配置設定が削除されて、次のディレクトリがクリアされます `var`.

読み取り： [Adobe Commerce ソフトウェアをアンインストールします](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall.html) 開発者向けドキュメントを参照してください。

Adobe Commerce ソフトウェアをアンインストールするには、次の手順に従います。

1. [環境に SSH で接続する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html).
1. 実行 `setup:uninstall` : `bin/magento setup:uninstall`
1. アンインストールを確認します。

次のメッセージが表示され、アンインストールが正常に完了したことを確認します。

```php
[SUCCESS]: Magento uninstallation complete.
```

つまり、Adobe Commerce（DB を含む）のインストールが本物の（Vanilla）状態に戻りました。

### 手順 2：をリセットする [!DNL git] 分岐

（を使用） [!DNL git] リセットすると、コードが過去に目的の状態に戻ります。

1. ローカル開発環境に環境のクローンを作成します。 Cloud Console で次のコマンドをコピーできます。    ![copy_git_clone.png](assets/copy_git_clone.png)
1. コミット履歴にアクセスします。 使用方法 `--reverse` 履歴を逆順に表示して利便性を高めるには： `git log --reverse`
1. 正常に動作しているコミットハッシュを選択します。 コードを本物の状態（Vanilla）にリセットするには、ブランチ（環境）を作成した最初のコミットを見つけます。
   ![Git コンソールでのコミットハッシュの選択](assets/select_commit_hash.png)
1. ハード適用 [!DNL git] リセット : `git reset --h <commit_hash>`
1. 変更をサーバーにプッシュ： `git push --force <origin> <branch>`

これらの手順を実行した後、 [!DNL git] ブランチがリセットされ、全体が [!DNL git] 変更ログは明確です。 最後 [!DNL git] プッシュトリガーは再デプロイしてすべての変更を適用し、Adobe Commerceを再インストールします。

## シナリオ 4：スナップショットなし、ビルドの中断（なし [!DNL SSH] 接続）

ここでは、環境が重大（critical）状態の場合に、環境をリセットする方法を説明します。デプロイメントプロシージャは動作しているアプリケーションを正常に構築できないため、次の処理が行われます [!DNL SSH] 接続できません。

このシナリオでは、まず以下を使用してAdobe Commerce アプリケーションの動作ステータスを復元する必要があります [!DNL git] をリセットしてから、Adobe Commerce ソフトウェアをアンインストールします（データベースをドロップして復元したり、デプロイメント設定を削除したりします）。 シナリオにはシナリオ 3 と同じステップが含まれますが、ステップの順序は異なり、追加のステップとして再デプロイが強制されます。 手順は次のとおりです。

1. [をリセット [!DNL git] 分岐。](/help/how-to/general/reset-environment-on-cloud.md#reset-git-branch)
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

を実行する場合 `setup:uninstall` コマンドがエラーで失敗し、完了できません。次の手順で DB を手動でクリアします。

1. [環境に SSH で接続する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html).
1. MySQL DB に接続します。 `mysql -h database.internal` （Pro 環境の場合は、以下を参照してください。 [MySQL サービスの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/mysql.html)）に設定します。
1. \&#39;main\&#39; DB をドロップします： `drop database main;`
1. 空の\&#39;main\&#39; DB を作成します： `create database main;`
1. 次の設定ファイルを削除します。 `config.php` , `config.php` , `.bak,` , `env.php`, `env.php.bak`

DB のリセット後、 [作る [!DNL git] 再デプロイをトリガーするために環境にプッシュ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/examples/example-using-cli.html) 新規作成した DB にAdobe Commerceをインストールします。 または [redeploy コマンドを実行する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html#environment-commands).
