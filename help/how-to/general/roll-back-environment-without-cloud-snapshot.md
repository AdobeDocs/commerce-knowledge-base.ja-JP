---
title: クラウドスナップショットを使用しない環境のロールバック
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境のスナップショットを作成することなく、環境をロールバックする 2 つのソリューションについて説明します。
exl-id: 834d13a7-3b1a-460c-9ed0-9d560105f436
feature: Build, Cloud, Console
source-git-commit: d7c714cf5b2f9db139440d814af26c12001bb4d9
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# クラウドスナップショットを使用しない環境のロールバック

この記事では、クラウドインフラストラクチャー上のAdobe Commerceで環境のスナップショットを作成することなく、環境をロールバックする 2 つのソリューションについて説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

お客様の状況に最も適したものを選択してください。

* 安定したビルドで、有効なスナップショットがない場合 – [ シナリオ 1：スナップショットがない、安定したビルド（SSH 接続が使用可能） ](#scen2)。
* ビルドが中断され、有効なスナップショットがない場合 – [ シナリオ 2：スナップショットなし、ビルドが中断（SSH 接続なし） ](#scen3)。

## シナリオ 1：スナップショットがなく、安定して構築（SSH 接続を使用可能） {#scen2}

ここでは、スナップショットを作成していないが、SSH 経由で環境にアクセスできる場合に、環境をロールバックする方法について説明します。

手順は次のとおりです。

1. 構成管理を無効にします。
1. Adobe Commerce ソフトウェアをアンインストールします。
1. Git ブランチをリセットします。

これらの手順を実行した後：

* Adobe Commerceのインストールがバニラ状態に戻ります（データベースが復元されました。デプロイメント設定が削除されました。`var` 下のディレクトリがクリアされました）
* git ブランチが過去に目的の状態にリセットされます

以下の詳細な手順を参照してください。

### 手順 0 （前提条件）:config.php を削除して、構成管理を無効にします {#disable_config_management}

デプロイメント中に以前の設定が自動的に適用されないように、設定管理を無効にする必要があります。

Configuration Management を無効にするには、`/app/etc/` ディレクトリに `config.php` （Adobe Commerce 2.4.x の場合）または `config.local.php` （Adobe Commerce 2.1.x の場合）のファイルが含まれていないことを確認してください。

設定ファイルを削除するには、次の手順に従います。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 設定ファイルを削除します。
   * Adobe Commerce 2.4 の場合：

   ```php
    rm app/etc/config.php
   ```

   * Adobe Commerce 2.1 の場合：

   ```php
     rm app/etc/config.local.php
   ```

開発者向けドキュメントの [ ストア設定の設定管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html) を確認して、設定管理について詳しく説明します。

### 手順 1: setup:uninstall コマンドを使用してAdobe Commerce ソフトウェアをアンインストールする {#setup-uninstall}


Adobe Commerce ソフトウェアをアンインストールすると、データベースが削除されて復元され、配置設定が削除されて、`var` の下のディレクトリがクリアされます。

開発者向けドキュメントの [Adobe Commerce ソフトウェアをアンインストールする ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall.html) を確認してください。

Adobe Commerce ソフトウェアをアンインストールするには、次の手順に従います。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. 実行 `setup:uninstall`:

   ```php
     php bin/magento setup:uninstall
   ```

1. アンインストールを確認します。

次のメッセージが表示され、アンインストールが正常に完了したことを確認します。

```php
[SUCCESS]: Magento uninstallation complete.
```

つまり、Adobe Commerce（DB を含む）のインストールが本物の（Vanilla）状態に戻りました。

### 手順 2:Git ブランチのリセット {#reset-git-branch}

Git をリセットすると、コードが以前に目的の状態に戻ります。

1. ローカル開発環境に環境のクローンを作成します。 Cloud Console で次のコマンドをコピーできます。    ![copy_git_clone.png](assets/copy_git_clone.png)
1. コミット履歴にアクセスします。 `--reverse` を使用して履歴を逆順に表示すると、より便利です。

   ```git
     git log --reverse
   ```

1. 正常に動作しているコミットハッシュを選択します。 コードを本物の状態（Vanilla）にリセットするには、ブランチ（環境）を作成した最初のコミットを見つけます。    ![Git コンソールでのコミットハッシュの選択 ](assets/select_commit_hash.png)
1. ハード Git リセットの適用：

   ```git
     git reset --h <commit_hash>
   ```

1. 変更をサーバーにプッシュ：

   ```git
     git push --force <origin> <branch>
   ```

これらの手順を実行すると、Git ブランチがリセットされ、Git の変更ログ全体がクリアされます。 最後の Git プッシュは、すべての変更を適用してAdobe Commerceを再インストールするために再デプロイすることをトリガーします。

## シナリオ 2：スナップショットがない、ビルドが破損している（SSH 接続がない） {#scen3}

ここでは、重要な状態の環境をロールバックする方法について説明します。デプロイ手順では、正常に動作するアプリケーションを構築できないため、SSH 接続が使用できなくなります。

このシナリオでは、まず Git リセットを使用してAdobe Commerce アプリケーションの動作ステータスを復元し、次にAdobe Commerce ソフトウェアをアンインストールして、データベースをドロップして復元したり、デプロイメント設定を削除したりします。 シナリオにはシナリオ 1 と同じステップが含まれますが、ステップの順序は異なり、追加のステップとして再デプロイが強制されます。 手順は次のとおりです。

[&#x200B;1. Git ブランチをリセットします。](/help/how-to/general/reset-environment-on-cloud.md#reset-git-branch)

[2。 構成管理を無効にします。](/help/how-to/general/reset-environment-on-cloud.md#disable_config_management)

[&#x200B;3. Adobe Commerce ソフトウェアをアンインストールします。](/help/how-to/general/reset-environment-on-cloud.md#setup-uninstall)

4&amp;period; Force redeploy.（強制再デプロイ）

これらの手順を実行すると、シナリオ 1 と同じ結果が得られます。

### 手順 4：再デプロイの強制

コミットを作成し（これは空のコミットである可能性がありますが、お勧めしません）、トリガーにプッシュして再デプロイします。

```git
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## セットアップに失敗した場合 :uninstall データベースを手動でリセットする

`setup:uninstall` コマンドの実行がエラーで失敗し、完了しない場合は、次の手順で DB を手動でクリアできます。

1. [ 環境に SSH で接続します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html)。
1. MySQL DB に接続します。

   ```sql
   mysql -h database.internal
   ```

1. `main` DB をドロップします。

   ```sql
   drop database main;
   ```

1. 空の `main` DB を作成します。

   ```sql
   create database main;
   ```

1. 設定ファイル `config.php`、`config.php` `.bak`、`env.php`、`env.php.bak` を削除します。

DB をリセットした後、[トリガーに Git プッシュを送信して環境を再デプロイ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html#git-commands)、新しく作成した DB にAdobe Commerceをインストールします。 または [redeploy コマンドを実行します ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli.html#environment-commands)。

## 関連資料

開発者向けドキュメントでは、

* [ クラウド上のスナップショットの復元 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots#restore-a-manual-backup)
* [ スナップショットの作成 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots#create-a-manual-backup)
* [ スナップショットとバックアップの管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots)
* [Cloud Console でのブランチの管理 – ログの表示 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/console-branches.html?lang=en#view-logs)
* [ コンポーネントのデプロイメントの失敗 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/deploy/recover-failed-deployment.html)
* [ プロジェクトの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-the-project)
