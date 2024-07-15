---
title: インストール後、画像とスタイルシートは読み込まれません。テキストのみが表示され、グラフィックは表示されません
description: この記事では、Adobe Commerceのインストール後にスタイルシートと画像が読み込まれない問題の理由と解決策について説明します。
exl-id: f33cee89-b416-4d63-8cc5-9cc57618ce92
feature: Install, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# インストール後、画像とスタイルシートは読み込まれません。テキストのみが表示され、グラフィックは表示されません

この記事では、Adobe Commerceのインストール後にスタイルシートと画像が読み込まれない問題の理由と解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.2.x, 2.3.x#キョウジ 2.2.x#
* Magento Open Source2.2.x, 2.3.x

## 問題

<u> 再現手順 </u>

1. Adobe Commerceをインストールします。
1. ストアフロントまたは管理者に移動します。

<u> 期待される結果 </u>

スタイルが適用されます。スタイルが見つからないような UI 要素はありません。

<u> 実際の結果 </u>

スタイルが正しく適用されず、グラフィックが欠落している。

## 原因：

ベース URL が正しくないか、サーバーの書き換え（CentOS、Ubuntu）が正しく設定されていないので、画像とスタイルシートへのパスが正しくありません。

その場合は、web ブラウザー検査を使用して静的アセットへのパスを確認し、それらのアセットがAdobe CommerceまたはMagento Open Sourceのファイルシステム上にあることを確認します。

静的アセットは、`frontend` ディレクトリと `adminhtml` ディレクトリ内の `<magento_root>/pub/static/` の下にあります。

## 解決策

使用しているソフトウェアと問題の原因に応じて、次のような解決策が考えられます。

* Apache web サーバーを使用している場合は、[server rewrites](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/apache.html#apache-help-rewrite) の設定と、Adobe Commerce/Magento Open Sourceサーバーのベース URL を確認して、もう一度試してください。 Apache `AllowOverride` ディレクティブの設定が正しくない場合は、静的ファイルが正しい場所から提供されません。
* nginx web サーバを使用している場合は、必ず [ 仮想ホスト ファイルを設定 ](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/nginx.html#configure-nginx-ubuntu) してください。 nginx 仮想ホストファイルは、次の条件を満たす必要があります。
   * `include` ディレクティブは、Adobe Commerce/Magento Open Sourceのインストールディレクトリにあるサンプル nginx 設定ファイルを指している必要があります。 例：    `include /var/www/html/magento2/nginx.conf.sample;`
   * `server_name` ディレクティブは、Adobe Commerce/Magento Open Sourceをインストールするときに指定したベース URL と一致する必要があります。 例：`server_name 192.186.33.10;`
* アプリケーションが [ 実稼動モード ](https://devdocs.magento.com/guides/v2.3/config-guide/bootstrap/magento-modes.html#production-mode) の場合は、`magento setup:static-content:deploy` コマンドを使用して静的ビューファイルをデプロイしてみてください。 静的ファイルのデプロイについて詳しくは、開発者ドキュメントの [ 静的ビューファイルのデプロイ ](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-subcommands-maint.html) を参照してください。
