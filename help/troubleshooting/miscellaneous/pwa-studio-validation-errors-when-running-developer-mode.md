---
title: PWA Studio：開発者モードの実行中に検証エラーが発生する
description: このトピックでは、以前に venia-concept （Venia はPWA ストアフロントです）環境ファイルを作成しなかった結果、Progressive Web App （PWA） Studio for Adobe Commerceで開発者モードを実行したときに検証エラーが発生した場合の解決策について説明します。 このファイルには、ローカル開発環境の変数が格納されます。
exl-id: 97d042ef-88e6-4eda-a834-2cff4de276e2
feature: Configuration
role: Developer
source-git-commit: 9d32a5971341ed8dc46e0932c10eaac4d17ec299
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# PWA Studio：開発者モードの実行中に検証エラーが発生する

このトピックでは、以前に venia-concept （Venia はPWA ストアフロントです）環境ファイルを作成しなかった結果、Progressive Web App （PWA） Studio for Adobe Commerceで開発者モードを実行したときに検証エラーが発生した場合の解決策について説明します。 このファイルには、ローカル開発環境の変数が格納されます。

## 影響を受ける製品とバージョン

* Adobe CommerceのPWA Studio

## 問題

<u> 再現手順 </u>:

* Adobe CommerceのPWA Studioで開発者モードを実行します。

<u> 期待される結果 </u>:

* PWA Studio サーバーは通常どおり起動します。

<u> 実際の結果 </u>:

* 検証エラーが表示されます。次のような内容になります。

```
    ⓧ  Missing required environment variables:         MAGENTO_BACKEND_URL: Connect to an instance of Adobe Commerce 2.3 by specifying its public domain name. (eg.         "https://master-7rqtwti-mfwmkrjfqvbjk.us-4.magentosite.cloud/")      ⚠  No .env file in ./packages/venia-concept. Autogenerate a .env file by running the command 'buildpack         create-env-file ./packages/venia-concept'.
```

## 原因：

お使いのローカル開発の環境変数ファイルがありません。 以下のコマンドで生成されるファイルには、ローカル開発環境用の変数が格納されます。

## 解決策

必ずコマンドを実行してください。

```
npx @magento/pwa-buildpack create-env-file packages/venia-concept
```

で設定します。ルートディレクトリに作成し、ローカル開発用の変数を保持するファイルを作成します。

## 関連資料

* [PWA Studio for Adobe Commerce ドキュメント &#x200B;](https://developer.adobe.com/commerce/pwa-studio/)
* [Venia ストアフロント（概念） &#x200B;](https://developer.adobe.com/commerce/pwa-studio/guides/packages/venia/)
