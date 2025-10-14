---
title: PHP 8.1 をサポートするバージョンにアップグレードする場合のデプロイ中のエラー
description: この記事では、PHP 8.1 をサポートするバージョンにアップグレードする場合に発生するエラーの解決策を示します。
exl-id: bdc4a355-4f2b-49a7-9c5d-63c950f7ca30
feature: Deploy, Observability
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# PHP 8.1 をサポートするバージョンにアップグレードする場合のデプロイ中のエラー

この記事では、PHP 8.1 をサポートするバージョンにアップグレードする場合に発生するエラーの解決策を示します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.4 以降のAdobe Commerce

* Extension または technology （Fastly、New Relicなど） version PHP 8.1

## 問題

PHP 8.1 をサポートするバージョンにアップグレードする場合、デプロイ中に次のエラーが発生します。

```PHP
{{E: Error parsing configuration files:

applications: Uncaught exception: The "json" extension is not supported for php:8.1
at <script>:109:12
throw("The \"" + unsupported_extensions[0] + "\" extension is not supported for " + service.type);
^
E: Error: Invalid configuration files, aborting build}}
```

## 原因：

PHP 8.1 には既に JSON のサポートが含まれており、拡張機能を個別にインストールする必要はありません。

## 解決策

`.magento.app.yaml` の **Runtime**/**Extensions** セクションから JSON を削除し、再デプロイします。

## 関連資料

開発者向けドキュメントの [PHP アプリケーション &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/app/php-settings)。
