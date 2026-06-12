---
title: PWA Studio：コンパイルを開始する前にWebpackがハングする
description: この記事では、Progressive Web App Studio （PWA Studio）でコンパイルを開始する前にJavaScript [Webpack] （https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/#webpack）が長い間停止する場合の推奨ソリューションについて説明します。
exl-id: 692eeafa-9289-4d66-9f2f-1e0fe36e681d
feature: Configuration
role: Developer
source-git-commit: 40766238a7ea748bff86decf75cddec28fe63bb9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# PWA Studio：コンパイルを開始する前にWebpackがハングする

この記事では、Progressive Web App Studio （PWA Studio）でコンパイルを開始する前に、JavaScript [Webpack](https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/#webpack)が長い間ハングする場合の推奨ソリューションについて説明します。

## 影響を受ける製品とバージョン

* PWA Studio

## イシュー

[pwa-buildpackの最新リリースが](https://github.com/magento/pwa-studio/tree/master/packages/pwa-buildpack)であること、および

```yaml
pwa-buildpack
```

バージョン番号は、`package.json` ファイル名リストの横に表示されます。 以前のバージョンの

```yaml
pwa-buildpack
```

プロジェクトの場合、webpackはコンパイルを開始する前に長い間停止する可能性があります。

<u>複製する手順</u>:

<u>前提条件</u>: VeniaなどのPWA Studio ストアフロントをローカルのAdobe Commerce インスタンスで設定し、を実行します

```yaml
build
```

または

```yaml
watch
```

コマンド。

<u>期待される結果</u>:

* `build` コマンドを使用する場合、Veniaのビルドアーティファクトが通常どおり生成されます。
* `watch` コマンドを使用すると、通常どおりVenia ストアフロントが開始されます。

<u>実際の結果</u>:

自分

```yaml
build
```

または

```yaml
watch
```

コマンドは停止しているように見え、完了せず、エラーも表示されません。

## 解決策

次のコマンドを使用してプロジェクトを更新します。

```yaml
yarn upgrade
```

次のコマンドを使用して、システムに最新バージョンのopensslがあることを確認します。

```yaml
openssl version
```

バージョンは1.0以上（OSX High Sierraの場合はLibreSSL 2）である必要があります。

OSXでは[Homebrew](https://brew.sh/)、Windowsでは[Chocolatey](https://chocolatey.org/)、またはLinux ディストリビューションのパッケージマネージャーを使用して、より高いバージョンのOpenSSLをインストールできます。

## 関連トピックス

* [Javascript Webpack：概念](https://webpack.js.org/concepts/)
* [Venia ストアフロントの設定](https://developer.adobe.com/commerce/pwa-studio/guides/packages/venia/)
* [PWA Buildpack](https://developer.adobe.com/commerce/pwa-studio/guides/packages/buildpack/)
* [buildpack コマンドラインインターフェイス](https://developer.adobe.com/commerce/pwa-studio/api/buildpack/cli/)
* [ツールとライブラリ：buildpack](https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/#webpack)
