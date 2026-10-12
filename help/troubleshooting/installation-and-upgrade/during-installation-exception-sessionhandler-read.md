---
title: インストール中に、例外SessionHandler::read （）
description: この記事では、Adobe Commerceのインストール時に発生する例外**SessionHandler::read （）** エラーの修正点を紹介します。
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%
---

# インストール中に、例外SessionHandler::read （）

この記事では、Adobe Commerceのインストール中に発生した例外&#x200B;**SessionHandler::read （）**&#x200B;のエラーに対する修正を説明します。

## イシュー

Adobe Commerceのインストールの最後の手順では、次の例外が表示されます。

```temrinal
exception 'Exception' with message 'Warning: SessionHandler::read():
open(..) failed: No such file or directory (2) ../magento2/lib/internal/Magento/Framework/Session/SaveHandler.php on line 74'
in ../magento2/lib/internal/Magento/Framework/App/ErrorHandler.php:67
```

>[!NOTE]
>
>このエラーは、2015年9月28日以前のコードバージョンでのみ発生します。 9月29日以降の日付のコードをインストールする場合、このエラーは発生しません。 Redisの設定オプションについて詳しくは、開発者ドキュメントの[Redis](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cache/redis/config-redis)の設定を参照してください。 コマンドラインインストーラーを使用してRedisを指定する方法について詳しくは、開発者ドキュメントの[&#x200B; インストールのトピック &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced)または[&#x200B; デプロイメント設定のトピック &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/deployment)を参照してください。

## 原因

これは、`session.save_handler` PHP パラメーターが`files`以外のセッションストレージ（`redis`、`memcached`など）に設定されている場合に発生します。 これは、私たちが解決するために取り組んでいる既知の問題です。

## 解決策：

* Adobe Commerce コードをアップグレードします。 開発者向けドキュメントの[&#x200B; インストールガイド/Adobe Commerce ソフトウェアの更新](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall)を参照してください。
* 既存のコードに対して次の回避策を使用します。

## `php.ini`を検索 {#locate-php-ini}

次のコマンドを入力して、`php.ini`を探します。

```php
php -i | grep "Loaded Configuration File"
```

一般的な場所は次のとおりです。

* Ubuntu: `/etc/php5/cli/php.ini`
* CentOS: `/etc/php.ini`

## 回避策 {#workaround}

1. `root`権限を持つユーザーは、テキストエディターで`php.ini`を開きます。
1. `session.save_handler`を検索
1. 次のいずれかの方法で設定します。
   * コメントアウトするには：

     ```php
     ;session.save_path = <path>
     ```

   * ファイルシステムのパスに設定するには：

     ```php
     session.save_handler = files
     ```
