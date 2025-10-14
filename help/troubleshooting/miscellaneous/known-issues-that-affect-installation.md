---
title: xdebug のインストールに影響する既知の問題
description: この記事では、オプションの PHP 拡張モジュール 'xdebug'を使用した際に例外エラーが発生した場合の解決策を提供します。
exl-id: 5090ea99-e0c3-436a-809b-109701740927
feature: Install
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# xdebug のインストールに影響する既知の問題

この記事では、オプションの PHP 拡張 `xdebug` 能を使用した際に例外エラーが発生した場合の解決策を示します。

* インストール中
* インストールが成功した後のCommerce管理者またはストアフロントへのアクセス

例外の例：

```php
Fatal error: Maximum function nesting level of '100' reached, aborting!
```

この問題を解決するには、次の操作を行います。

* `xdebug` 拡張機能を無効にします。
* `xdebug.max_nesting_level` の値を 200 以上の値に設定します。 詳しくは、[xdebug ドキュメント &#x200B;](http://xdebug.org/docs/basic#max_nesting_level) を参照してください。

`xdebug` の設定を変更または無効にした後、Apache を再起動します。

* CentOS: `sudo service httpd restart`
* Ubuntu: `sudo service apache2 restart`
