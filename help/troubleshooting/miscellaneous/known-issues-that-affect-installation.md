---
title: xdebug のインストールに影響する既知の問題
description: この記事では、オプションの PHP 拡張モジュール 'xdebug'を使用した際に例外エラーが発生した場合の解決策を提供します。
exl-id: 5090ea99-e0c3-436a-809b-109701740927
feature: Install
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# xdebug のインストールに影響する既知の問題

この記事では、オプションの PHP 拡張機能を使用した際に例外エラーが発生した場合の解決策を示します `xdebug`.

* インストール中
* インストールが成功した後のCommerce管理者またはストアフロントへのアクセス

例外の例：

```php
Fatal error: Maximum function nesting level of '100' reached, aborting!
```

この問題を解決するには、次の操作を行います。

* を無効にする `xdebug` 拡張機能。
* 次の値を設定 `xdebug.max_nesting_level` 200 以上の値に設定します。 詳しくは、を参照してください [xdebug ドキュメント](http://xdebug.org/docs/basic#max_nesting_level).

の設定を変更したり無効にした後 `xdebug`で、Apache を再起動します。

* CentOS: `sudo service httpd restart`
* Ubuntu: `sudo service apache2 restart`
