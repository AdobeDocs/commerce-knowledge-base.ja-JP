---
title: Redis のシリアル化解除エラー'setup:static-content:deploy'
description: この記事では、「magento setup:static-content:deploy」を実行する際の Redis のシリアル化解除エラーを修正します。
exl-id: 4bc88933-3bf9-4742-b864-b82d3c1b07a9
feature: Cache, Deploy, Page Content, SCD, Services, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Redis のシリアル化解除エラー `setup:static-content:deploy`

この記事では、`magento setup:static-content:deploy` を実行する際の Redis のシリアル化解除エラーの修正について説明します。

`magento setup:static-content:deploy` を実行すると、Redis エラーが発生します。

```
[Exception]
Notice: unserialize(): Error at offset 0 of 1 bytes in
/var/www/domain.com/vendor/magento/module-config/App/Config/Type/System.php on line 214
```

この問題は、Redis 接続の並列干渉プロセスによって発生します。

解決するには、次の環境変数を設定して、`setup:static-content:deploy` をシングルスレッドモードで実行します。

```
STATIC_CONTENT_THREADS =1
```

または、`setup:static-content:deploy` コマンドに続いて `-j 1` （または `--jobs=1`）引数を実行します。

マルチスレッドを無効にすると、静的なアセットをデプロイするプロセスが遅くなります。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス：2.1.2 以降
* クラウドインフラストラクチャー 2.1.2 以降でのAdobe Commerce
* Redis （任意のバージョン）

## 問題

`setup:static-content:deploy` コマンドを実行すると、Redis エラーが発生します。

```php
)
[2017-06-02 19:57:59] Command:php ./bin/magento setup:static-content:deploy --jobs=3  en_US

[Exception]

Notice: unserialize(): Error at offset 0 of 1 bytes in /app/<domain>/vendor/magento/module-config/App/Config/Type/System.php
on line 214

.....

[CredisException]
read error on connection

[RedisException]
read error on connection

.....

[Exception]

Notice: unserialize(): Error at offset 0 of 1 bytes in /app/<domain>/vendor/magento/module-config/App/Config/Type/System.php
on line 214

.....

[RuntimeException]
Command php ./bin/magento setup:static-content:deploy --jobs=3  en_US  returned code 3
```

## 原因：

この問題は、Redis 接続上のプロセスが並行して干渉することが原因です。

ここでは、`App/Config/Type/System.php` のプロセスが `system_defaultweb` に対する応答を期待していましたが、別のプロセスが行った `system_cache_exists` に対する応答を受け取りました。 詳しくは [Jason Woods&#39; post](https://github.com/magento/magento2/issues/9287#issuecomment-302362283) を参照してください。

## 解決策

次の環境変数を設定して、並列処理を無効にし、シングルスレッドモードで `setup:static-content:deploy` を実行します。

```
STATIC_CONTENT_THREADS =1
```

また、`setup:static-content:deploy` コマンドの後に `-j 1` （または `--jobs=1`）引数を指定して実行することもできます。

>[!NOTE]
>
>シングルスレッドモードでは、静的コンテンツのデプロイメントプロセスに 4 倍の時間がかかる場合があります。

## 詳細情報

開発者向けドキュメントでは、

* [Redis の設定 ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html?lang=ja)
* [ コマンドラインアップグレード ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html?lang=ja)
