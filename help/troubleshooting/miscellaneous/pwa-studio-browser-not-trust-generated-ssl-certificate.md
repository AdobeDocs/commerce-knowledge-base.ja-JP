---
title: 「PWA Studio：ブラウザーが生成された SSL 証明書を信頼しない」
description: この記事では、開発中にPWA Studioストアフロントのローカルインスタンスに移動した際に、ブラウザーで生成される信頼できない SSL 証明書の警告に対するソリューションを説明します。
exl-id: b7bfe1e6-5832-4472-9e51-f04b8583428a
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# PWA Studio：生成された SSL 証明書がブラウザーで信頼されない

この記事では、開発中にPWA Studioストアフロントのローカルインスタンスに移動した際に、ブラウザーで生成される信頼できない SSL 証明書の警告に対するソリューションを説明します。

## 影響を受ける製品とバージョン

Adobe CommerceのPWA Studio

## 問題

ブラウザーは、生成されたローカルPWA Studioストアフロントの SSL 証明書を信頼しません。

## 原因：

開発/ステージングサイトへの参照。

## 解決策

ストアフロントプロジェクトで、コマンドを実行して、ローカル開発インスタンスにカスタムホスト名と SSL 証明書を追加します。

```sh
yarn buildpack create-custom-origin ./
```

証明書の生成は [devcert](https://github.com/davewasmer/devcert) によって処理されます。 OpenSSL によって異なるので、次のコマンドを使用してシステムに現在のバージョンの openssl があることを確認します。

`openssl version`

バージョンは 1.0 以上（OSX High Sierra の場合は LibreSSL 2）にする必要があります。

OSX の [Homebrew](https://brew.sh/)、Windows の [Chocolatey](https://chocolatey.org/) または Linux ディストリビューションのパッケージマネージャーを使用して、より新しいバージョンの OpenSSL をインストールできます。

Linux を実行している場合は、`libnss3-tools` （または同等のツール）がシステムにインストールされていることを確認します。 詳細については、[devcert](https://github.com/davewasmer/devcert#skipcertutil) readme のこのセクションで説明しています。

一部のユーザーは、トリガー証明書の再生成のために devcert フォルダーを削除することを推奨しています。

* macOS ユーザーの場合、通常このフォルダーは `{{~/Library/Application Support/devcert }}` にあります。
* Windows ユーザーの場合、通常、このフォルダーは `${User}\AppData\Local\devcert` にあります。

## サポートナレッジベースの関連資料

* [PWA Studio：自己署名証明書の信頼エラー ](https://support.magento.com/hc/en-us/articles/360038973172)
* [PWA Studio: コンパイルを開始する前に webpack がハングします](/help/troubleshooting/miscellaneous/pwa-studio-webpack-hangs-before-beginning-compilation.md)
* [PWA Studio：ブラウザーに「Cannot proxy to」エラーが表示される](/help/troubleshooting/miscellaneous/pwa-studio-browser-displays-cannot-proxy-to-error.md)
* [PWA Studio：開発者モードの実行中に検証エラーが発生する](/help/troubleshooting/miscellaneous/pwa-studio-validation-errors-when-running-developer-mode.md)
