---
title: PHP 8.1をサポートするバージョンにアップグレードする際にデプロイメント中にエラーが発生する
description: この記事では、PHP 8.1をサポートするバージョンにアップグレードする際にデプロイメント中に発生するエラーの解決策を提供します。
exl-id: bdc4a355-4f2b-49a7-9c5d-63c950f7ca30
feature: Deploy, Observability
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%
---
# PHP 8.1をサポートするバージョンにアップグレードする際にデプロイメント中にエラーが発生する

この記事では、PHP 8.1をサポートするバージョンにアップグレードする際にデプロイメント中に発生するエラーの解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.4.4. その後

* 拡張機能やテクノロジー（Fastly、New Relicなど） バージョン PHP 8.1

## イシュー

PHP 8.1をサポートするバージョンにアップグレードする際に、デプロイメント中に次のエラーが発生します。

```PHP
{{E: Error parsing configuration files:

applications: Uncaught exception: The "json" extension is not supported for php:8.1
at <script>:109:12
throw("The \"" + unsupported_extensions[0] + "\" extension is not supported for " + service.type);
^
E: Error: Invalid configuration files, aborting build}}
```

## 原因

PHP 8.1にはJSON サポートが既に含まれており、拡張機能を個別にインストールする必要はありません。

## Solution

`.magento.app.yaml`の&#x200B;**Runtime** > **Extensions** セクションからJSONを削除して、再デプロイします。

## 関連トピックス

開発者ドキュメントの[PHP アプリケーション &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings)。
