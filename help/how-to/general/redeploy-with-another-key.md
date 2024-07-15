---
title: 'クラウド上のAdobe Commerce：認証キーの変更と再デプロイ'
description: この記事では、様々な認証キーを使用してクラウドインフラストラクチャにAdobe Commerceを再デプロイする方法について説明します。 例えば、別のアカウントでキーを使用した場合や、Adobe Commerceのキーの代わりにMagento Open Sourceのキーを使用した場合などです。
exl-id: 47407c81-5c52-406f-812f-6c6b3ca5cafa
feature: Cloud, Deploy
source-git-commit: f11c8944b83e294b61d9547aefc9203af344041d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# クラウド上のAdobe Commerce：認証キーを変更して再デプロイ

この記事では、様々な認証キーを使用してクラウドインフラストラクチャにAdobe Commerceを再デプロイする方法について説明します。 例えば、別のアカウントでキーを使用した場合や、Adobe Commerceのキーの代わりにMagento Open Sourceのキーを使用した場合などです。

誤ったキーを使用すると、デプロイメントが失敗します。 復元するには、プロジェクトのクローンを作成し、正しいキーを `auth.json` に追加して、変更をマスターブランチにプッシュする必要があります。

この記事では、プロジェクトには `master` ブランチのみ（プロジェクトを最初に作成した際のデフォルトのブランチは `master`）があると仮定します。

正しい認証キーを使用して再デプロイするには：

1. クラウドインフラストラクチャ上にAdobe Commerceがあるマシンに SSH キーでログインします。
1. プロジェクトへのログイン

   ```
   magento-cloud login
   ```

1. `auth` という名前でコードを更新するブランチを作成します。

   ```
   magento-cloud environment:branch auth master
   ```

1. プロジェクトのルートディレクトリに移動します。
1. `auth.json` をテキストエディターで開きます。

   ```json
   {
      "http-basic": {
         "repo.magento.com": {
            "username": "<your public key>",
            "password": "<your private key>"
         }
      }
   }
   ```

1. 正しい認証キーを追加します。
1. 変更を保存し、テキストエディターを終了します。
1. 変更内容をコミットして結合します。

   ```
   git add -A
   ```

   ```
   git commit -m "<description of change>"
   ```

   ```
   git push origin master
   ```

1. デプロイメントが完了するまで待ちます。

デプロイメントが成功したかどうかを示すメッセージが表示されます。 画面に表示される **環境ルート** の 1 つに移動すると、デプロイメントが成功したことを確認できます。
