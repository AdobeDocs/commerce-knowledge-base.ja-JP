---
title: Web ブラウザーでAdobe Commerceにアクセスする際に 503 エラーが発生する
description: この記事では、Adobe Commerce ストアフロントや管理者にアクセスしようとすると 503 エラーが発生する問題の解決策を提供します。
exl-id: 4232aa21-40c2-41b0-9fb0-fc8cd4db8e39
feature: Storefront
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Web ブラウザーでAdobe Commerceにアクセスする際に 503 エラーが発生する

この記事では、Adobe Commerce ストアフロントや管理者にアクセスしようとすると 503 エラーが発生する問題の解決策を提供します。

## 影響を受ける製品とバージョン

Adobe Commerce 2.3.x

## 問題 {#symptoms}

<u> 再現手順 </u>

（前提条件：ストアが [ メンテナンスモード ](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-mode.html#config-mode-show)）になっていないことを確認します。

Web ブラウザーでCommerce管理者またはストアフロントに移動します。

<u> 期待される結果 </u>

ページが読み込まれます。

<u> 実際の結果 </u>

HTTP 503 （サービスを利用できません）エラーが発生する。 Apache `error.log` には次のメッセージが含まれます。

*無効なコマンド「Order」です。スペルミスがあるか、サーバー設定に含まれていないモジュールによって定義されている可能性があります。*

## 原因： {#details}

Apache 2.4 互換モジュール `mod_access_compat` が無効になっているため、Adobe Commerce URL の書き換えが正しく機能しません。

## 解決策 {#suggested-solution}

`mod_access_compat` Apache モジュールを有効にし、「root」権限を持つユーザーとして次のコマンドを実行して、Apache を再起動します。

```bash
a2enmod access_compat
service <name> restart
```

CentOS の場合

```bash
<name>
```

等しい

```bash
httpd
```

.Ubuntu の場合

```bash
<name>
```

等しい

```bash
apache2
```

。

## 関連資料 {#additional-resources}

* [mod\_access\_compat に関する Apache ドキュメント ](https://httpd.apache.org/docs/current/mod/mod_access_compat.html)
* [mod\_authz\_host に関する Apache ドキュメント ](https://httpd.apache.org/docs/current/mod/mod_authz_host.html)
* [Apache Definitive Guide からの Order、Allow、Deny](https://docstore.mik.ua/orelly/linux/apache/ch05_06.htm)
* [askubuntu.com](https://askubuntu.com/questions/335228/changes-in-apache-config-between-12-04-2-and-12-04-3-lts)
