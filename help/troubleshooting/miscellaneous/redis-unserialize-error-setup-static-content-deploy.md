---
title: Redis のシリアル化解除エラー'設定:static-content:デプロイ'
description: この記事では、「magento セットアップ」の実行時に発生する Redis のシリアル化解除エラーを修正します:static-content:デプロイ'.
exl-id: 4bc88933-3bf9-4742-b864-b82d3c1b07a9
feature: Cache, Deploy, Page Content, SCD, Services, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Redis のシリアル化解除エラー `setup:static-content:deploy`

この記事では、の実行時の Redis のシリアル化解除エラーを修正します `magento setup:static-content:deploy`.

実行中 `magento setup:static-content:deploy` Redis エラーを引き起こします。

```
[Exception]
Notice: unserialize(): Error at offset 0 of 1 bytes in
/var/www/domain.com/vendor/magento/module-config/App/Config/Type/System.php on line 214
```

この問題は、Redis 接続の並列干渉プロセスによって発生します。

解決するには、を実行します `setup:static-content:deploy` シングルスレッドモードでは、次の環境変数を設定します。

```
STATIC_CONTENT_THREADS =1
```

または、 `setup:static-content:deploy` コマンドの後に `-j 1` （または `--jobs=1` ）引数。

マルチスレッドを無効にすると、静的なアセットをデプロイするプロセスが遅くなります。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス：2.1.2 以降
* クラウドインフラストラクチャー 2.1.2 以降でのAdobe Commerce
* Redis （任意のバージョン）

## 問題

の実行 `setup:static-content:deploy` コマンドが原因で Redis エラーが発生します。

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

ここでは、のプロセスです `App/Config/Type/System.php` は、に対する応答を期待していました `system_defaultweb`が、次の応答を受信しました： `system_cache_exists` それは別の工程で作られた。 詳しくは、で説明を参照してください [ジェイソン・ウッズの地位](https://github.com/magento/magento2/issues/9287#issuecomment-302362283).

## 解決策

並列処理を無効にして実行 `setup:static-content:deploy` シングルスレッドモードでは、次の環境変数を設定します。

```
STATIC_CONTENT_THREADS =1
```

を実行することもできます。 `setup:static-content:deploy` コマンドの後に `-j 1` （または `--jobs=1`）引数。

>[!NOTE]
>
>シングルスレッドモードでは、静的コンテンツのデプロイメントプロセスに 4 倍の時間がかかる場合があります。

## 詳細情報

開発者向けドキュメントでは、

* [Redis の設定](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html)
* [コマンドラインアップグレード](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html)
