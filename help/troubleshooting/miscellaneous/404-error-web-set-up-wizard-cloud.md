---
title: 管理パネルから Web セットアップウィザードにアクセスすると、404 エラーが見つからない
description: この記事では、管理パネルから Web セットアップウィザードにアクセスしようとしたときに 404 が見つからないというエラーが発生した場合の解決策について説明します。
exl-id: 1b89da58-c872-481b-b2a0-aa48db8223db
feature: Admin Workspace, Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

<u> 再現手順 </u>:

マーチャントは、Web セットアップウィザードをクリックして、新しいモジュール/統合をインストールします。

<u> 期待される結果 </u>:

モジュール/統合のインストール

<u> 実際の結果 </u>:

404 エラーが表示される。

## 原因：

Web セットアップウィザードは、クラウドインフラストラクチャインスタンス上のすべてのAdobe Commerceで無効になっています。有効にすることはできません。 Composer を使用して拡張機能をインストールする必要があります。

## 解決策

この機能は、クラウドインフラストラクチャー上のAdobe Commerceでは無効になっています。

アドビのクラウドインフラストラクチャでAdobe Commerceの更新を実行したり、外部モジュールをインストールしたりする方法について詳しくは、開発者向けドキュメントの [ 拡張機能のインストール、管理、アップグレード ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions) を参照してください。
アップデートの実行方法やAdobe Commerce オンプレミス用の外部モジュールのインストール方法については、開発者向けドキュメントの [ クイックスタートインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/composer) を参照してください。

## 関連資料

* 開発者向けドキュメントの [ 拡張機能のインストール ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension) を参照してください。
