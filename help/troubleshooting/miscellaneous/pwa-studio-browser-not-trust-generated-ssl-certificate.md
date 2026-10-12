---
title: PWA Studio：生成されたSSL証明書がブラウザーで信頼されない
description: この記事では、開発中にPWA Studio ストアフロントのローカルインスタンスに移動する際に、ブラウザーで生成された信頼できないSSL証明書の警告に対する解決策を提供します。
exl-id: b7bfe1e6-5832-4472-9e51-f04b8583428a
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
source-wordcount: '303'
ht-degree: 0%
---
# PWA Studio：生成されたSSL証明書がブラウザーで信頼されない

この記事では、開発中にPWA Studio ストアフロントのローカルインスタンスに移動する際に、ブラウザーで生成された信頼できないSSL証明書の警告に対する解決策を提供します。

## 影響を受ける製品とバージョン

PWA Studio for Adobe Commerce

## イシュー

ブラウザーは、ローカルのPWA Studio ストアフロントの生成されたSSL証明書を信頼しません。

## 原因

開発/ステージングサイトへの参照。

## Solution

ストアフロントプロジェクトで、カスタムホスト名とSSL証明書をローカル開発インスタンスに追加するコマンドを実行します。

```sh
yarn buildpack create-custom-origin ./
```

証明書の生成は[devcert](https://github.com/davewasmer/devcert)によって処理されます。 OpenSSLに依存するので、次のコマンドを使用して、システムに最新バージョンのopensslがあることを確認してください。

`openssl version`

バージョンは1.0以上（OSX High Sierraの場合はLibreSSL 2）である必要があります。

OSXでは[Homebrew](https://brew.sh/)、Windowsでは[Chocolatey](https://chocolatey.org/)、またはLinux ディストリビューションのパッケージマネージャーを使用して、より高いバージョンのOpenSSLをインストールできます。

Linuxを実行している場合は、`libnss3-tools` （または同等のもの）がシステムにインストールされていることを確認してください。 詳しくは、[devcert](https://github.com/davewasmer/devcert#skipcertutil) readmeのこの節を参照してください。

一部のユーザーは、証明書の再生成をトリガーするためにdevcert フォルダーを削除することを提案しています。

* MacOS ユーザーの場合、このフォルダーは通常`{{~/Library/Application Support/devcert }}`にあります
* Windows ユーザーの場合、このフォルダーは通常`${User}\AppData\Local\devcert`にあります

## サポートナレッジベースの関連情報

* [PWA Studio：自己署名証明書の信頼エラー](https://support.magento.com/hc/en-us/articles/360038973172)
* [PWA Studio：コンパイルを開始する前にWebpackがハングする](/help/troubleshooting/miscellaneous/pwa-studio-webpack-hangs-before-beginning-compilation.md)
* [PWA Studio：ブラウザーに「次にプロキシできません」というエラーが表示される](/help/troubleshooting/miscellaneous/pwa-studio-browser-displays-cannot-proxy-to-error.md)
* [PWA Studio：開発者向けモードの実行時に検証エラーが発生する](/help/troubleshooting/miscellaneous/pwa-studio-validation-errors-when-running-developer-mode.md)
