---
title: Adobe Commerce クラウド版：認証キーの変更と再デプロイ
description: この記事では、様々な認証キーを使用してクラウドインフラストラクチャ上にAdobe Commerceを再デプロイする方法について説明します。 例えば、別のアカウントでキーを使用した場合や、Adobe Commerce キーの代わりにMagento Open Source キーを使用した場合があります。
exl-id: 47407c81-5c52-406f-812f-6c6b3ca5cafa
feature: Cloud, Deploy
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%
---
# Adobe Commerce クラウド版：認証キーの変更と再デプロイ

この記事では、様々な認証キーを使用してクラウドインフラストラクチャ上にAdobe Commerceを再デプロイする方法について説明します。 例えば、別のアカウントでキーを使用した場合や、Adobe Commerce キーの代わりにMagento Open Source キーを使用した場合があります。

正しくないキーを使用した場合、デプロイメントは失敗します。 回復するには、プロジェクトを複製し、正しいキーを`auth.json`に追加し、変更をマスターブランチにプッシュする必要があります。

この記事では、プロジェクトに`master` ブランチのみが含まれていると仮定します（最初にプロジェクトを作成する際のデフォルトブランチは`master`です）。

正しい認証キーを使用して再デプロイするには：

1. Adobe Commerce on cloud infrastructureのSSH キーを持つコンピューターにログインします。
1. プロジェクトにログインします。

   ```
   magento-cloud login
   ```

1. 名前`auth`のコードを更新するブランチを作成します：

   ```
   magento-cloud environment:branch auth master
   ```

1. プロジェクトのルートディレクトリに移動します。
1. `auth.json`をテキストエディターで開きます。

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
1. 変更をコミットして結合します。

   ```
   git add -A
   ```

   ```
   git commit -m "<description of change>"
   ```

   ```
   git push origin master
   ```

1. デプロイメントが完了するのを待ちます。

メッセージは、デプロイメントが成功したかどうかを示します。 画面に表示されている&#x200B;**環境ルート**&#x200B;のいずれかに移動することで、デプロイメントが成功したことを確認できます。
