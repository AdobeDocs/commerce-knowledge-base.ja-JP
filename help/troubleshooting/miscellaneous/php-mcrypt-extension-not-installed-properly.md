---
title: PHP mcrypt 拡張モジュールが正しくインストールされていません
description: PHP mcrypt 拡張モジュールが正しくインストールされていません
exl-id: 1010349e-6631-4a05-8883-5cc903d67534
feature: Extensions, Install
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# PHP mcrypt 拡張モジュールが正しくインストールされていません

>[!WARNING]
>
>注意：mcrypt ライブラリ機能は [PHP 7.1 から非推奨となり、PHP 7.2 から削除されました ](https://www.php.net/manual/en/intro.mcrypt.php)。

## 詳細

エラーには次のものがあります。

```php
exception 'Exception' with message 'PHP Warning: PHP Startup: Unable to load dynamic library '/usr/lib/php5/20121212/mcrypt.so' - /usr/lib/php5/20121212/mcrypt.so: cannot open shared object file: No such file or directory
```

```php
Installing data fixtures:
/usr/bin/php -f '/Users/username/www/magento/dev/shell/run_data_fixtures.php' -- --bootstrap='MAGE_DIRS[base][path]=/Users/username/www/magento' 2>&1
[ERROR] exception 'Exception' with message '
Fatal error: Uncaught exception 'Exception' with message 'Module 'Magento_Core' depends on 'mcrypt' PHP [extension](https://experienceleague.adobe.com/en/docs/commerce-operations/operational-playbook/glossary#extension) that is not loaded.'
```

```php
======================================================================
   The application has thrown an exception!
======================================================================
 Magento\Framework\Exception
 Command returned non-zero exit code:
`/usr/bin/php5 -f '/var/www/magento2/dev/shell/run_data_fixtures.php' -- --bootstrap='MAGE_DIRS[base][path]=/var/www/magento2' 2>&1`
```

## 説明

特に、オペレーティングシステムとは別の Linux/Apache/MySQL/PHP （LAMP）「スタック」を含む開発者システムでは、mcrypt がまったくインストールされていないか、LAMP スタックのパスにインストールされていて、オペレーティングシステムのパスにはインストールされていない可能性があります。

その結果、Adobe Commerce インストーラーで拡張機能が見つからず、インストールが失敗します。

## 提案

mcrypt 拡張機能が次のいずれかの方法で読み込まれているかどうかを確認します。

* Web サーバーのルートディレクトリに [phpinfo.php](http://kb.mediatemple.net/questions/764/How+can+I+create+a+phpinfo.php+page%3F#gs) ファイルをセットアップし、web ブラウザーで出力を調べます。
* 次のコマンドを実行します。    `$ php -r "phpinfo();" | grep mcrypt`

mcrypt がインストールされて *ない* 場合、次のようなメッセージが表示されます。

```php
PHP Warning:  PHP Startup: Unable to load dynamic library '/usr/lib/php5/20121212/mcrypt.so' - /usr/lib/php5/20121212/mcrypt.so: cannot open shared object file: No such file or directory in Unknown on line 0
```

場合によっては、[ コマンドライン ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced) からAdobe Commerce ソフトウェアをインストールし、mcrypt がインストールされている LAMP スタックへのフルパスを指定する必要があります。
