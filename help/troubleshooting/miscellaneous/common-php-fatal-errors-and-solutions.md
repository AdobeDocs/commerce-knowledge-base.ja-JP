---
title: 一般的なPHPの致命的なエラーと解決策
description: この記事では、Adobe Commerceのログを調べるときに見つかる一般的なPHP Fatal Errorの簡単な例と、それらが示す問題の解決策を示します。
exl-id: 3e42d38f-97bc-4d38-8e36-23b1453f81d9
feature: Support
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: a59f76dc-e003-5617-951e-dffa5bd3de81
    internal-label: Support
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%
---
# 一般的なPHPの致命的なエラーと解決策

この記事では、Adobe Commerceのログを調べるときに見つかる一般的なPHP Fatal Errorの簡単な例と、それらが示す問題の解決策を示します。

## 例

*&#39;PHPの致命的なエラー：60秒の最大実行時間が…&#39;*&#x200B;を超えています

## Solution

`php.ini` ファイルでカスタム `max_execution_time`値を設定して再デプロイすることで、最大実行時間を更新できます。

例：

`max_execution_time = 120`

[php.ini設定のカスタマイズ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings)の記事を参照してください。

## 例

*&#39;PHPの致命的なエラー：メモリ サイズが792723456 バイトを使い果たしました&#39;* （これはバイト サイズの例です）。

## Solution

`php.ini`の設定をカスタマイズします。 この[php.ini設定のカスタマイズ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings)記事を参照してください。

## 例

*&#39;PHP警告：不明：ストリームを開けませんでした：そのようなファイルまたはディレクトリはありません&#39;*

## Solution

`php.ini` ファイルのWindows スタイルの末尾を削除しないでください。 Windowsでは、改行（ASCII 0x0dまたは\r）と改行（\n）の組み合わせで改行が終了します。これはCR/LFとも呼ばれます。

## 例

*&#39;PHPの致命的なエラー：PDOExceptionが見つかりません：SQLSTATE\[HY000\] \[1040\]接続が&#39;*&#x200B;に多すぎます

## Solution

MySQL環境のディスク容量が不足しています。 MySQL環境にディスク容量を増やします。

## 例

*&#39;PHPの致命的なエラー：見つからないTypeError: Magento&#39;*&#x200B;の戻り値

## Solution

`<root>/tmp` ディレクトリが空いていることを確認してください。 完全な場合は、ディレクトリにスペースを追加します。 これには、ファイルを別のディレクトリに移動したり、削除したりするだけです。

## 関連トピックス

アドビの開発者ドキュメントには、次のようなものがあります。

* [PHP設定エラー](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/overview)
* [必要なPHP設定](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/php-settings)
* [Redis検証](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cache/redis/redis-session#verify-redis-connection)
* [Redisの設定](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cache/redis/config-redis)
* [PHP メモリ制限エラー](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/overview)
* [一般的な問題の解決策 – メモリ制限](https://developer.adobe.com/commerce/testing/guide/unit/command-line#solutions-to-common-problems)
