---
title: 統合環境のパフォーマンスが低い
description: この記事では、Pro 統合環境とスターターのステージング環境のパフォーマンスが低下している問題の解決策を説明します。
feature: Integration, Staging
role: Developer
exl-id: 46110dbc-2f54-4654-95e2-39e8ae1e6979
source-git-commit: 139c2836ba36686357c7a5458a36550c7b1273c1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 統合環境のパフォーマンスが低い

この記事では、Pro 統合環境とスターターのステージング環境のパフォーマンスが低下している問題の解決策を説明します。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

Pro 統合環境またはスターターステージング環境のパフォーマンスが低下しています。

## 原因：

カタログやデータのサイズ、またはサードパーティの統合やカスタマイズの要件によっては、統合環境で使用可能なリソースを超えている可能性があります。

## 解決策

パフォーマンスの問題に対処するには、統合環境のベストパフォーマンスのベストプラクティスに従っていることを確認します。 また、統合を強化するために、環境のアップグレードをリクエストする必要が生じる場合もあります。

まず、お使いの環境が [&#x200B; 拡張統合設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27242) 上にあるかどうかを確認します。

* [Pro アーキテクチャ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment)
* [&#x200B; スターターアーキテクチャ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#staging-environment)

次のいずれかの方法を使用して、デプロイメントログを確認します。

### メソッド 1:

Cloud CLI を使用して次のコマンドを実行します。

`magento-cloud activity:log -e <branch name>`

### メソッド 2:

[Cloud Console](https://console.adobecommerce.com) でその環境の最新のデプロイメントログを確認します。

デプロイメントログの最後に、このような情報が表示された場合は、最初の行に size=XL、残りの行に size=L と表示され、Enhanced Integration の設定になっていることを意味します。

```
Environment configuration
mymagento (type: php:8.2, size: XL, disk: 5120)
mysql (type: mysql:10.6, size: L, disk: 5120)
redis (type: redis:7.2, size: L)
opensearch (type: opensearch:2, size: L, disk: 1024)
rabbitmq (type: rabbitmq:3.12, size: L, disk: 1024)
```

拡張統合設定を使用していない場合は、[&#x200B; 機能強化/アップグレードをリクエスト &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27242) できます。
拡張統合設定を既に使用している場合や、アップグレード後もパフォーマンスの問題が発生する場合は、統合環境で最適なパフォーマンスを得るために、必ず次のベストプラクティスに従ってください。

* [Pro アーキテクチャ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment)
* [&#x200B; スターターアーキテクチャ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#staging-environment)

上記の推奨事項を満たしている場合は、[&#x200B; サポートリクエストを送信 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) して追加のサポートを受けてください。
