---
title: PWA Studio：開発者向けモードの実行時に検証エラーが発生する
description: このトピックでは、以前にvenia-conceptを作成しなかった結果として、Adobe Commerce用のProgressive Web App （PWA） Studioでデベロッパーモードを実行する際に検証エラーが発生した場合の解決策について説明します（VeniaはPWA ストアフロントです）。 環境ファイル。 このファイルには、ローカル開発環境の変数が格納されます。
exl-id: 97d042ef-88e6-4eda-a834-2cff4de276e2
feature: Configuration
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%
---
# PWA Studio：開発者向けモードの実行時に検証エラーが発生する

このトピックでは、以前にvenia-conceptを作成しなかった結果として、Adobe Commerce用のProgressive Web App （PWA） Studioでデベロッパーモードを実行する際に検証エラーが発生した場合の解決策について説明します（VeniaはPWA ストアフロントです）。 環境ファイル。 このファイルには、ローカル開発環境の変数が格納されます。

## 影響を受ける製品とバージョン

* PWA Studio for Adobe Commerce

## イシュー

<u>再現する手順</u>:

* Adobe Commerce用PWA Studioで開発者モードを実行します。

<u>期待される結果</u>:

* PWA Studio サーバーは正常に起動します。

<u>実際の結果</u>:

* 検証エラーが表示されます。これは次のようになります。

```
    ⓧ  Missing required environment variables:         MAGENTO_BACKEND_URL: Connect to an instance of Adobe Commerce 2.3 by specifying its public domain name. (eg.         "https://master-7rqtwti-mfwmkrjfqvbjk.us-4.magentosite.cloud/")      ⚠  No .env file in ./packages/venia-concept. Autogenerate a .env file by running the command 'buildpack         create-env-file ./packages/venia-concept'.
```

## 原因

ローカル開発環境の環境変数ファイルがありません。 次のコマンドが生成するファイルには、ローカル開発環境の変数が格納されます。

## Solution

必ずコマンドを実行してください

```
npx @magento/pwa-buildpack create-env-file packages/venia-concept
```

ローカル開発環境の変数を保持するファイルを生成するために、ルートディレクトリに保存します。

## 関連トピックス

* [PWA Studio for Adobe Commerceのドキュメント](https://developer.adobe.com/commerce/pwa-studio/)
* [Venia Storefront （コンセプト）](https://developer.adobe.com/commerce/pwa-studio/guides/packages/venia/)
