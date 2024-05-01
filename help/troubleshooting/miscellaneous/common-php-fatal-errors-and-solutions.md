---
title: 一般的な PHP の致命的なエラーと解決策
description: この文書では、Adobe Commerceのログを調べた際に見つかるであろう一般的な PHP Fatal Error の簡単な例と、それらが示す問題の解決策を示します。
exl-id: 3e42d38f-97bc-4d38-8e36-23b1453f81d9
feature: Support
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 一般的な PHP の致命的なエラーと解決策

この文書では、Adobe Commerceのログを調べた際に見つかるであろう一般的な PHP Fatal Error の簡単な例と、それらが示す問題の解決策を示します。

## 例

*「PHP 致命的エラー：最大実行時間の 60 秒を超過しました…」*

## 解決策

カスタムを設定することで、最大実行時間を更新できます `max_execution_time` の値 `php.ini` ファイルを作成して再デプロイします。

例：

`max_execution_time = 120`

を参照してください [php.ini の設定をカスタマイズする](https://devdocs.magento.com/cloud/project/magento-app-php-ini.html) 記事。

## 例

*「PHP 致命的エラー：許可されているメモリサイズ （792723456 バイトを超えています）」* （これは単なるバイトサイズの例です。）

## 解決策

のカスタマイズ `php.ini` 設定。 こちらを参照 [php.ini の設定をカスタマイズする](https://devdocs.magento.com/cloud/project/magento-app-php-ini.html) 記事。

## 例

*「PHP 警告：不明：ストリームを開けませんでした：そのようなファイルまたはディレクトリがありません」*

## 解決策

で Windows スタイルの終端を削除しないようにしてください `php.ini` ファイル。 Windows では、改行は改行（CR/LF とも呼ばれる）とキャリッジリターン（ASCII 0x0d または\r）の組み合わせで終端されます。

## 例

*&#39;PHP 致命的エラー：キャッチされない PDOException: SQLSTATE\[HY000\] \[1040\] の接続が多すぎます&#39;*

## 解決策

MySQL 環境のディスク領域が不足しています。 MySQL 環境に追加のディスク領域を提供します。

## 例

*「PHP 致命的エラー：キャッチされない TypeError:Magentoの戻り値」*

## 解決策

を確認します `<root>/tmp` ディレクトリは、おそらくいっぱいだからです。 一杯の場合は、ディレクトリに空き領域を増やします。 これには、単にファイルを別のディレクトリに移動したり、削除したりすることが含まれます。

## 関連資料

開発者向けドキュメントでは、

* [PHP 設定エラー](https://devdocs.magento.com/guides/v2.3/install-gde/trouble/php/tshoot_php-set.html)
* [必要な PHP 設定](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html)
* [Redis 検証](https://devdocs.magento.com/guides/v2.3/config-guide/redis/redis-session.html#redis-verify)
* [Redis の設定](https://devdocs.magento.com/guides/v2.3/config-guide/redis/config-redis.html)
* [PHP メモリ制限エラー](https://devdocs.magento.com/guides/v2.3/install-gde/trouble/php/tshoot_php-set.html#trouble-php-memory)
* [一般的な問題の解決策 – メモリ制限](https://devdocs.magento.com/guides/v2.3/test/unit/unit_test_execution_cli.html#solutions-to-common-problems)
