---
title: 管理パネルから Web セットアップウィザードにアクセスすると、404 エラーが見つからない
description: この記事では、管理パネルから Web セットアップウィザードにアクセスしようとしたときに 404 が見つからないというエラーが発生した場合の解決策について説明します。
exl-id: 1b89da58-c872-481b-b2a0-aa48db8223db
feature: Admin Workspace, Cloud, Paas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 管理パネルから Web セットアップウィザードにアクセスすると、404 エラーが見つからない

この記事では、管理パネルから Web セットアップウィザードにアクセスしようとしたときに 404 が見つからないというエラーが発生した場合の解決策について説明します。

## 影響を受ける製品とバージョン

* Web セットアップウィザード機能は、Adobe Commerce（すべてのデプロイメント方法） 2.3.6 で非推奨となり、2.4.0 で削除されました。

## 問題

Web セットアップウィザードを使用して拡張機能をインストールすると、404 ページが表示されます。

<u>再現手順</u>:

マーチャントは、Web セットアップウィザードをクリックして、新しいモジュール/統合をインストールします。

<u>期待される結果</u>:

モジュール/統合のインストール

<u>実際の結果</u>:

404 エラーが表示される。

## 原因：

Web セットアップウィザードは、クラウドインフラストラクチャインスタンス上のすべてのAdobe Commerceで無効になっています。有効にすることはできません。 Composer を使用して拡張機能をインストールする必要があります。

## 解決策

この機能は、クラウドインフラストラクチャー上のAdobe Commerceでは無効になっています。

参照： [拡張機能のインストール、管理、アップグレード](https://devdocs.magento.com/cloud/howtos/install-components.html) アドビのクラウドインフラストラクチャでAdobe Commerceの更新を実行する方法や外部モジュールをインストールする方法については、開発者向けドキュメントを参照してください。
参照： [クイックスタートインストール](https://devdocs.magento.com/guides/v2.3/install-gde/composer.html) Adobe Commerce オンプレミスの更新を実行する方法や外部モジュールをインストールする方法については、開発者向けドキュメントを参照してください。

## 関連資料

* 参照： [拡張機能のインストール](https://devdocs.magento.com/cloud/howtos/install-components.html#install-an-extension) 開発者向けドキュメントを参照してください。
