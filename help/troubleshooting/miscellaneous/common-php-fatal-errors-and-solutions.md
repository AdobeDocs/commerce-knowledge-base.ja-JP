---
title: 一般的な PHP の致命的なエラーと解決策
description: この文書では、Adobe Commerceのログを調べた際に見つかるであろう一般的な PHP Fatal Error の簡単な例と、それらが示す問題の解決策を示します。
exl-id: 3e42d38f-97bc-4d38-8e36-23b1453f81d9
feature: Support
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 一般的な PHP の致命的なエラーと解決策

この文書では、Adobe Commerceのログを調べた際に見つかるであろう一般的な PHP Fatal Error の簡単な例と、それらが示す問題の解決策を示します。

## 例

*&#39;PHP 致命的エラー：60 秒の最大実行時間を超過しました…&#39;*

## 解決策

実行時間の最大値を更新するには、`php.ini` ファイルでカスタム `max_execution_time` の値を設定し、再配置します。

例：

`max_execution_time = 120`

[php.ini の設定をカスタマイズする ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/app/php-settings) の記事を参照してください。

## 例

*&#39;PHP Fatal error: 792723456 バイトのメモリサイズが使い果たされました&#39;* （これは単なるバイトサイズの例です。

## 解決策

`php.ini` 設定をカスタマイズします。 この [php.ini の設定をカスタマイズする ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/app/php-settings) の記事を参照してください。

## 例

*&#39;PHP 警告：不明：ストリームを開けませんでした：そのようなファイルまたはディレクトリがありません&#39;*

## 解決策

`php.ini` ファイル内の Windows スタイルの終端を削除しないようにしてください。 Windows では、改行は改行（CR/LF とも呼ばれる）とキャリッジリターン（ASCII 0x0d または\r）の組み合わせで終端されます。

## 例

*&#39;PHP 致命的エラー：PDOException がキャッチされていません：SQLSTATE\[HY000\] \[1040\] 接続が多すぎます&#39;*

## 解決策

MySQL 環境のディスク領域が不足しています。 MySQL 環境に追加のディスク領域を提供します。

## 例

*&#39;PHP 致命的なエラー：Uncaught TypeError: Magentoの戻り値&#39;*

## 解決策

`<root>/tmp` ディレクトリが満杯である可能性があるので、確認してください。 一杯の場合は、ディレクトリに空き領域を増やします。 これには、単にファイルを別のディレクトリに移動したり、削除したりすることが含まれます。

## 関連資料

開発者向けドキュメントでは、

* [PHP 設定エラー ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/overview)
* [ 必要な PHP 設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings)
* [Redis 検証 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cache/redis/redis-session#verify-redis-connection)
* [Redis の設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cache/redis/config-redis)
* [PHP メモリ制限エラー ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/overview)
* [ 一般的な問題の解決策 – メモリ制限 ](https://developer.adobe.com/commerce/testing/guide/unit/command-line/#solutions-to-common-problems)
