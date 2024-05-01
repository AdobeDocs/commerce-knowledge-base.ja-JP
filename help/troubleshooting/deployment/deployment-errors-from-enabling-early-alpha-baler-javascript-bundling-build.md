---
title: 早期アルファ版ベラーモジュールを有効にした場合のデプロイメントエラー
description: この機能は現在、アルファ開発の初期の段階にあるので、マーチャントが実稼動環境でベーラーモジュールを使用すると、デプロイメントエラーが発生します。
exl-id: 6cdac0a5-eaeb-467d-8369-9017aed6219e
feature: Build, Deploy, Extensions, SCD, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# 早期アルファ版ベラーモジュールを有効にした場合のデプロイメントエラー

この機能は現在、アルファ開発の初期の段階にあるので、マーチャントが実稼動環境でベーラーモジュールを使用すると、デプロイメントエラーが発生します。

>[!WARNING]
>
>初期アルファ版の JavaScript バンドルは、実稼動用の準備ができておらず、自己責任で使用されます。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.3.x および 2.4.x 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.3.x および 2.4.x

## 問題

現在アルファ開発の初期の段階にあるので、マーチャントが実稼動環境で Baler モジュールを使用することはお勧めしません。 使用すると、デプロイメントエラーが発生する場合があります。

<u>再現手順</u>:

1. 商人はカードを挿入しようとします **SCD\_USE\_BALER** のビルドステージの変数 `.magento.env.yaml` ファイル。Baler JavaScript バンドル パッケージを有効にします。
1. マーチャントは、Baler Composer の依存関係も追加します。 `"magento/module-baler": "1.0.0-alpha"` 対象： `require` セクション `composer.json`.

<u>期待される結果</u>:

正常なデプロイメント。

<u>実際の結果</u>:

マーチャントは、クラウドのデプロイメントログに次のようなエラーメッセージを表示します。 `<project home>/var/log/cloud.log`静的コンテンツのデプロイステージで、次の操作をおこないます。

```
[2020-08-19 12:06:12] WARNING: [1007] Baler JS bundling cannot be used because of the following issues:
        [2020-08-19 12:06:12] WARNING:  - Path to baler executable could not be found. The Node package may not be installed or may not be linked.
```

## 原因：

Baler モジュールは現在、アルファ開発の初期段階にあり、Baler 拡張機能のインストールプロセスは複雑です。

## 解決策

既存の BalerAlphaドキュメントは、次の場所で確認できます。 [Github/Magento/Baler/アルファの基本を学ぶ](https://github.com/magento/baler/blob/master/docs/ALPHA.md). ただし、実稼動での使用の準備は整っておらず、自己責任で使用します。 代わりに、ファイルの最適化のために、Adobe Commerceの組み込みバンドル（基本バンドル）を使用して、JavaScript （JS）ファイルを結合またはバンドルすることをお勧めします。

* 管理者で結合またはバンドルをオンにできます（結合とバンドルは同時に有効にできません）。 **ストア** > **設定** > **設定** > **詳細** > **開発者** > **JavaScript 設定**.
* コマンドラインからAdobe Commerceの組み込みバンドル（基本バンドル）を有効にすることもできます。 `php -f bin/magento config:set dev/js/enable_js_bundling 1`

詳しくは、次を参照してください [クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerceでの CSS と JavaScript ファイルの最適化](https://support.magento.com/hc/en-us/articles/360044482152).
