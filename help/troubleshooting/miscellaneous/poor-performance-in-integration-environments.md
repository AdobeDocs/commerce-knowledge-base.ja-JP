---
title: 統合環境でのパフォーマンスの低下
description: この記事では、Pro統合環境とスターターステージング環境のパフォーマンスが低下している問題に対する解決策を提供します。
feature: Integration, Staging
role: Developer
exl-id: 46110dbc-2f54-4654-95e2-39e8ae1e6979
source-git-commit: 139c2836ba36686357c7a5458a36550c7b1273c1
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 統合環境でのパフォーマンスの低下

この記事では、Pro統合環境とスターターステージング環境のパフォーマンスが低下している問題に対する解決策を提供します。

## 影響を受ける製品とバージョン：

* Adobe Commerce on cloud infrastructure （すべてのバージョン）

## イシュー

Pro統合環境またはスターターステージング環境のパフォーマンスが低い。

## 原因

カタログやデータのサイズ、またはサードパーティの統合やカスタマイズの要件によっては、統合環境で利用可能なリソースが超過している可能性があります。

## Solution

パフォーマンスの問題に対処するには、統合環境でのベストパフォーマンスのベストプラクティスに従っていることを確認します。 また、統合を強化するために、環境のアップグレードをリクエストする必要がある場合もあります。

まず、環境が[拡張統合設定](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27242)上にあるかどうかを確認します。

* [プロアーキテクチャ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment)
* [スターターアーキテクチャ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#staging-environment)

次のいずれかの方法を使用して、デプロイメントログを確認します。

### 方法1:

Cloud CLIを使用して次のコマンドを実行します。

`magento-cloud activity:log -e <branch name>`

### 方法2:

[Cloud Console](https://console.adobecommerce.com)でその環境の最新のデプロイメントログを確認します。

デプロイメントログの最後に、次のような表示が表示された場合（最初の行はsize=XL、残りの行はsize=L）、これは拡張統合設定を使用していることを意味します。

```
Environment configuration
mymagento (type: php:8.2, size: XL, disk: 5120)
mysql (type: mysql:10.6, size: L, disk: 5120)
redis (type: redis:7.2, size: L)
opensearch (type: opensearch:2, size: L, disk: 1024)
rabbitmq (type: rabbitmq:3.12, size: L, disk: 1024)
```

拡張統合設定を使用していない場合は、[拡張/アップグレードをリクエストできます](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27242)。
拡張統合設定を既に使用している場合、またはアップグレード後もパフォーマンスの問題が発生する場合は、統合環境で最適なパフォーマンスを実現するためのベストプラクティスに従ってください。

* [プロアーキテクチャ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment)
* [スターターアーキテクチャ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#staging-environment)

上記の推奨事項を満たした場合は、[追加支援のためにサポートリクエスト &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)を送信してください。
