---
title: インストールは約70%で停止します
description: この記事では、インストールが約70%で停止した場合の修正について説明します。
exl-id: 04aa3572-3c42-4565-9f7f-b4d90df96df2
feature: Install, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%
---
# インストールは約70%で停止します

この記事では、インストールが約70%で停止した場合の修正について説明します。

## イシュー

セットアップウィザードを使用したインストール中に、プロセスは約70%で停止します（サンプルデータの有無にかかわらず）。 画面にエラーは表示されません。

## 原因

この問題の一般的な原因は次のとおりです。

* [`max_execution_time`](http://php.net/manual/en/info.configuration.php#ini.max-execution-time)のPHP設定
* nginxとVarnishのタイムアウト値

## 解決策：

次の項目をすべて適切に設定します。

### すべてのweb サーバーとVarnish {#all-web-servers-and-varnish}

1. [`phpinfo.php`](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software) ファイルを使用して、`php.ini`を探します。
1. `root`権限を持つユーザーは、テキストエディターで`php.ini`を開きます。
1. `max_execution_time`設定を探します。
1. 値を`18000`に変更します。
1. 変更を`php.ini`に保存して、テキストエディターを終了します。
1. Apacheを再起動します。

   * CentOS: `service httpd restart`
   * Ubuntu: `service apache2 restart`

   nginxまたはVarnishを使用する場合は、次の節に進みます。

### nginxのみ {#nginx-only}

nginxを使用する場合は、付属の`nginx.conf.sample`を使用するか、次のように`location ~ ^/setup/index.php` セクションにnginx ホスト設定ファイルのタイムアウト設定を追加します。

```php
location ~ ^/setup/index.php {
    .....................
    fastcgi_read_timeout 600s;
       fastcgi_connect_timeout 600s;
}
```

nginxを再起動：`service nginx restart`

### ニスのみ {#varnish-only}

Varnishを使用する場合は、`default.vcl`を編集し、次のように`backend` スタンザにタイムアウト制限値を追加します。

```php
backend default {
.....................
      .first_byte_timeout = 600s;
}
```

Varnishを再起動します。

```php
service varnish restart
```
