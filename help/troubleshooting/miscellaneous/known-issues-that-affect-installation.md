---
title: xdebug インストールに影響する既知の問題
description: この記事では、オプションのPHP拡張機能「xdebug」を使用する際に例外エラーが発生した場合の解決策を提供します。
exl-id: 5090ea99-e0c3-436a-809b-109701740927
feature: Install
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# xdebug インストールに影響する既知の問題

この記事では、オプションのPHP拡張機能`xdebug`を使用する際に例外エラーが発生した場合の解決策を紹介します。

* インストール中
* インストールが成功した後にCommerce管理者またはストアフロントにアクセスする

例外の例：

```php
Fatal error: Maximum function nesting level of '100' reached, aborting!
```

この問題を解決するには、次の操作を行います。

* `xdebug`拡張機能を無効にします。
* `xdebug.max_nesting_level`の値を200以上に設定します。 詳しくは、[xdebug ドキュメント ](http://xdebug.org/docs/basic#max_nesting_level)を参照してください。

`xdebug`の設定を変更または無効にした後、Apacheを再起動します。

* CentOS: `sudo service httpd restart`
* Ubuntu: `sudo service apache2 restart`
