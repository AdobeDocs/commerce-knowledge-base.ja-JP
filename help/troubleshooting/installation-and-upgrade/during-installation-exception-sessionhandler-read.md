---
title: インストール中、例外 SessionHandler::read （）
description: 「この記事では、Adobe Commerceのインストール中に例外**SessionHandler::read （）**が発生した場合の対処方法について説明します。」
source-git-commit: 5cec04f8c4f80d34fc26b06eb929960ce21e2dc0
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# インストール中、例外 SessionHandler::read （）

この記事では、Adobe Commerceのインストール中に発生した例外 **SessionHandler::read （）** エラーを修正します。

## 問題

Adobe Commerceをインストールするための最後の手順で、次の例外が表示されます。

```temrinal
exception 'Exception' with message 'Warning: SessionHandler::read():
open(..) failed: No such file or directory (2) ../magento2/lib/internal/Magento/Framework/Session/SaveHandler.php on line 74'
in ../magento2/lib/internal/Magento/Framework/App/ErrorHandler.php:67
```

>[!NOTE]
>
>このエラーは、2015 年 9 月 28 日（PT）より前のコードバージョンでのみ発生します。 9 月 29 日以降の日付のコードをインストールする場合、このエラーは発生しません。 Redis の設定オプションについて詳しくは、開発者向けドキュメントの [Redis の設定 ](https://devdocs.magento.com/guides/v2.3/config-guide/redis/config-redis.html) を参照してください。 コマンドラインインストーラーを使用して Redis を指定する方法については、開発者向けドキュメントの [ インストールトピック ](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-install.html) または [ デプロイメント設定トピック ](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-subcommands-deployment.html#instgde-cli-subcommands-configphp) を参照してください。

## 原因：

これは、`session.save_handler` の PHP パラメータが `files` 以外のセッションストレージ（たとえば、`redis`、`memcached` など）に設定されている場合に発生します。 これは、解決に向けて取り組んでいる既知の問題です。

## ソリューション：

* Adobe Commerce コードをアップグレードします。 開発者向けドキュメントの [ インストールガイド/Adobe Commerce ソフトウェアのアップデート ](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update) を参照してください。
* 既存のコードで次の回避策を使用します。

## `php.ini` を見つけます {#locate-php-ini}

次のコマンドを入力して、`php.ini` を見つけます。

```php
php -i | grep "Loaded Configuration File"
```

典型的な位置は次の通りです。

* Ubuntu: `/etc/php5/cli/php.ini`
* CentOS: `/etc/php.ini`

## 回避策 {#workaround}

1. `root` 権限を持つユーザーとして、`php.ini` をテキストエディターで開きます。
1. `session.save_handler` を見つけます
1. 次のいずれかの方法で設定します。
   * コメントアウトするには：

     ```php
     ;session.save_path = <path>
     ```

   * ファイルシステムパスに設定するには：

     ```php
     session.save_handler = files
     ```
