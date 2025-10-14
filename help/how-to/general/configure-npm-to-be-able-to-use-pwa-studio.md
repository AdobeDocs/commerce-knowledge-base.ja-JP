---
title: PWA Studioを使用できるように NPM を設定する
description: '[Progressive Web Apps （PWA） Studio] （https://magento.github.io/pwa-studio/）は、Cloud Infrastructure 2.3.x 以降のAdobe Commerceで使用できる新しいプロジェクトです。 PWA Studioを使用してインストールするには、NPM パッケージマネージャーのバージョンを 5.x 以降に設定して、Node.js 8.x がサポートされるようにする必要があります。これは、「.magento.app.yaml」設定ファイルの「hooks:build」セクションで行われます。'
exl-id: 3854fc94-e8ad-45d8-bf3e-73462364220d
source-git-commit: 139c2836ba36686357c7a5458a36550c7b1273c1
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# PWA Studioを使用できるように NPM を設定する

[&#x200B; プログレッシブ web アプリケーション（PWA） Studio](https://magento.github.io/pwa-studio/) は、Cloud Infrastructure 2.3.x 以降のAdobe Commerceで使用できる新しいプロジェクトです。 PWA Studioを使用してインストールするには、NPM パッケージマネージャーのバージョンを 5.x 以降に設定して、Node.js 8.x がサポートされるようにする必要があります。これは、`hooks:build` 設定ファイルの `.magento.app.yaml` セクションで行います。

## 環境とテクノロジー

* クラウドインフラストラクチャー 2.3.X 上のAdobe Commerce
* Adobe CommerceのPWA

## NPM バージョンの設定：手順

必要な NPM バージョンを設定するには、`.magento.app.yaml` 設定ファイルで指定します。 次の手順に従います。

1. ローカル開発環境で、`.magento.app.yaml` 設定ファイルを見つけます。
1. プレーンテキストエディターまたは IDE を使用して編集するファイルを開きます。
1. `hooks:build` のセクションで、必要なバージョンを設定します。 次の例では、現時点で最高（2019 年 2 月 4 日（PT））の NPM v9.5.0 をインストールするように設定されています。

   ```yaml
   hooks:
       build: |
           unset NPM_CONFIG_PREFIX
           curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
           export NVM_DIR="$HOME/.nvm"
           [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
           nvm install 9.5.0
   ```

   >[!NOTE]
   >
   >ビルドだけでなく、アプリケーションで Node.JS を実行する場合は、次のコマンドを追加してビルドフックを変更してください。
   > 
   > ```
   > echo 'unset NPM_CONFIG_PREFIX' >> .environment
   > echo 'export NO_UPDATE_NOTIFIER=1' >> .environment
   > echo 'export NVM_DIR="$MAGENTO_CLOUD_DIR/.nvm"' >> .environment
   > echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> .environment
   > ```

1. 変更をファイルに保存します。
1. Git が編集したファイルを [&#x200B; 統合環境 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27242) にプッシュします。

変更は、更新された YAML ファイルを Git によって環境にプッシュした後に有効になります。

## 関連ドキュメント

* Adobe Commerce on Cloud Infrastructure ガイドの [&#x200B; アプリケーション設定：フック &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property.html?lang=ja)。
