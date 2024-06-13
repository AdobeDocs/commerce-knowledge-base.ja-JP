---
title: インストール中、例外 SessionHandler::read （）
description: 「この記事では、Adobe Commerceのインストール中に例外**SessionHandler::read （）**が発生した場合の対処方法について説明します。」
source-git-commit: 5cec04f8c4f80d34fc26b06eb929960ce21e2dc0
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# インストール中、例外 SessionHandler::read （）

この記事では、例外の解決策について説明します **SessionHandler::read （）** Adobe Commerceのインストール中にエラーが発生しました。

## 問題

Adobe Commerceをインストールするための最後の手順で、次の例外が表示されます。

```temrinal
exception 'Exception' with message 'Warning: SessionHandler::read():
open(..) failed: No such file or directory (2) ../magento2/lib/internal/Magento/Framework/Session/SaveHandler.php on line 74'
in ../magento2/lib/internal/Magento/Framework/App/ErrorHandler.php:67
```

>[!NOTE]
>
>このエラーは、2015 年 9 月 28 日（PT）より前のコードバージョンでのみ発生します。 9 月 29 日以降の日付のコードをインストールする場合、このエラーは発生しません。 Redis の設定オプションの詳細については、を参照してください。 [Redis の設定](https://devdocs.magento.com/guides/v2.3/config-guide/redis/config-redis.html) 開発者向けドキュメントを参照してください。 コマンドラインインストーラーを使用して Redis を指定する方法については、を参照してください。 [インストールトピック](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-install.html) または [デプロイメント設定トピック](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-subcommands-deployment.html#instgde-cli-subcommands-configphp) 開発者向けドキュメントを参照してください。

## 原因：

これは、 `session.save_handler` PHP パラメータは、次の値とは別のセッションストレージに設定されます。 `files` （例： `redis`, `memcached`など）。 これは、解決に向けて取り組んでいる既知の問題です。

## ソリューション：

* Adobe Commerce コードをアップグレードします。 こちらを参照してください [インストールガイド / Adobe Commerce ソフトウェアのアップデート](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update) 開発者向けドキュメントを参照してください。
* 既存のコードで次の回避策を使用します。

## を見つける `php.ini` {#locate-php-ini}

を見つける `php.ini` 次のコマンドを入力します。

```php
php -i | grep "Loaded Configuration File"
```

典型的な位置は次の通りです。

* Ubuntu: `/etc/php5/cli/php.ini`
* CentOS: `/etc/php.ini`

## 回避策 {#workaround}

1. を使用した As a ユーザー `root` 権限、開く `php.ini` テキストエディター。
1. を見つける `session.save_handler`
1. 次のいずれかの方法で設定します。
   * コメントアウトするには：

     ```php
     ;session.save_path = <path>
     ```

   * ファイルシステムパスに設定するには：

     ```php
     session.save_handler = files
     ```
