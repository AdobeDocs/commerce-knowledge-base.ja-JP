---
title: 'PWA Studio: コンパイルを開始する前に Webpack がハングします'
description: ここでは、Progressive Web App Studio （PWA Studio）でコンパイルを開始する前に JavaScript [Webpack] （https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/#webpack）が長時間停止した場合の解決策について説明します。
exl-id: 692eeafa-9289-4d66-9f2f-1e0fe36e681d
feature: Configuration
role: Developer
source-git-commit: 032fe4d32921c63570672b9c68e8c03e00bd1077
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# PWA Studio: コンパイルを開始する前に Webpack がハングします

この記事では、Progressive Web App Studio （PWA Studio[ でコンパイルを開始する前に JavaScript](https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/#webpack)Webpack）が長時間停止した場合の解決策について説明します。

## 影響を受ける製品とバージョン

* PWA Studio

## 問題

[pwa-buildpack の最新リリースが何であるかを確認します ](https://github.com/magento/pwa-studio/tree/master/packages/pwa-buildpack)。

```yaml
pwa-buildpack
```

バージョン番号は、`package.json` ファイル名のリストの横に表示されます。 古いバージョンの

```yaml
pwa-buildpack
```

プロジェクト。webpack は、コンパイルを開始する前に長時間停止する可能性があります。

<u> 再現手順 </u>:

<u> 前提条件 </u>：ローカルのAdobe Commerce インスタンスを使用して、Venia などのPWA Studio ストアフロントを設定して

```yaml
build
```

または

```yaml
watch
```

コマンド。

<u> 期待される結果 </u>:

* を使用する場合    ```yaml    build    ```    コマンドを使用すると、通常は Venia のビルドアーティファクトが生成されます。
* を使用する場合    ```yaml    watch    ```    コマンドを実行すると、Venia ストアフロントが通常どおり開始されます。

<u> 実際の結果 </u>:

あなたの

```yaml
build
```

または

```yaml
watch
```

コマンドが停止しているように見え、完了せず、エラーも表示されません。

## 解決策

次のコマンドを使用してプロジェクトを更新します。

```yaml
yarn upgrade
```

次のコマンドを使用して、システムに現在のバージョンの openssl があることを確認します。

```yaml
openssl version
```

バージョンは 1.0 以上（OSX High Sierra の場合は LibreSSL 2）にする必要があります。

OSX の [Homebrew](https://brew.sh/)、Windows の [Chocolatey](https://chocolatey.org/) または Linux ディストリビューションのパッケージマネージャーを使用して、より新しいバージョンの OpenSSL をインストールできます。

## 関連資料

* [Javascript Webpack：概念 ](https://webpack.js.org/concepts/)
* [Venia ストアフロントのセットアップ ](https://developer.adobe.com/commerce/pwa-studio/guides/packages/venia/)
* [PWA Buildpack](https://developer.adobe.com/commerce/pwa-studio/guides/packages/buildpack/)
* [buildpack コマンドラインインターフェイス ](https://developer.adobe.com/commerce/pwa-studio/api/buildpack/cli/)
* [ ツールとライブラリ：buildpack](https://developer.adobe.com/commerce/pwa-studio/guides/project/tools-libraries/#webpack)
