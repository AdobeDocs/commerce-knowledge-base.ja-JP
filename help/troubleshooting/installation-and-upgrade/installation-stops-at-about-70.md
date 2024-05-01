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

* の PHP 設定 [`max_execution_time`](http://php.net/manual/en/info.configuration.php#ini.max-execution-time)
* Nginx と Varnish のタイムアウト値

## 解決策：

必要に応じて、次の設定をすべて行います。

### すべての Web サーバーとワニス {#all-web-servers-and-varnish}

1. を見つけます。 `php.ini` の使用 [`phpinfo.php`](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/optional.html#install-optional-phpinfo) ファイル。
1. を使用した As a ユーザー `root` 権限、開く `php.ini` テキストエディター。
1. を見つけます。 `max_execution_time` の設定値。
1. 値をに変更します `18000` .
1. 変更をに保存します。 `php.ini` をクリックして、テキストエディターを終了します。
1. Apache を再起動します。

   * CentOS: `service httpd restart`
   * Ubuntu: `service apache2 restart`

   Nginx または Varnish を使用する場合は、次の節に進みます。

### nginx のみ {#nginx-only}

nginx をご利用の場合は、含まれているを使用してください `nginx.conf.sample` または、nginx ホスト設定ファイルのタイムアウト設定を `location ~ ^/setup/index.php` セクションを次のように設定します。

```php
location ~ ^/setup/index.php {
    .....................
    fastcgi_read_timeout 600s;
       fastcgi_connect_timeout 600s;
}
```

nginx を再起動します。 `service nginx restart`

### ワニスのみ {#varnish-only}

ニスを使用する場合は、次のように編集します。 `default.vcl` にタイムアウト制限値を追加します。 `backend` stanza は次のように記述します。

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
