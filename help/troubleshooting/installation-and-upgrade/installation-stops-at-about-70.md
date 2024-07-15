---
title: インストールが約 70 % で停止
description: この記事では、インストールが約 70% 停止した場合の修正方法を説明します。
exl-id: 04aa3572-3c42-4565-9f7f-b4d90df96df2
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# インストールが約 70 % で停止

この記事では、インストールが約 70% 停止した場合の修正方法を説明します。

## 問題

セットアップ ウィザードを使用したインストール中、プロセスは約 70% で停止します（サンプル データの有無は問わない）。 画面にエラーは表示されません。

## 原因：

この問題の一般的な原因は次のとおりです。

* [`max_execution_time`](http://php.net/manual/en/info.configuration.php#ini.max-execution-time) の PHP 設定
* Nginx と Varnish のタイムアウト値

## 解決策：

必要に応じて、次の設定をすべて行います。

### すべての Web サーバーとワニス {#all-web-servers-and-varnish}

1. [`phpinfo.php`](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/optional.html#install-optional-phpinfo) ファイルを使用して `php.ini` を見つけます。
1. `root` 権限を持つユーザーとして、`php.ini` をテキストエディターで開きます。
1. `max_execution_time` 設定を見つけます。
1. その値を `18000` に変更します。
1. `php.ini` への変更を保存し、テキストエディターを終了します。
1. Apache を再起動します。

   * CentOS: `service httpd restart`
   * Ubuntu: `service apache2 restart`

   Nginx または Varnish を使用する場合は、次の節に進みます。

### nginx のみ {#nginx-only}

nginx を使用する場合は、次のように、付属の `nginx.conf.sample` を使用するか、nginx ホスト構成ファイルのタイムアウト設定を `location ~ ^/setup/index.php` セクションに追加します。

```php
location ~ ^/setup/index.php {
    .....................
    fastcgi_read_timeout 600s;
       fastcgi_connect_timeout 600s;
}
```

nginx を再起動します：`service nginx restart`

### ワニスのみ {#varnish-only}

Varnish を使用する場合は、次のように `default.vcl` を編集し、`backend` のスタンザにタイムアウト制限値を追加します。

```php
backend default {
.....................
      .first_byte_timeout = 600s;
}
```

ワニスを再起動します。

```php
service varnish restart
```
