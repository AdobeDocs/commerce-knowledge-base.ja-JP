---
title: クラウドインスタンスにサードパーティのアプリケーションをインストールできますか？
description: いいえ。 クラウドインフラストラクチャサーバー上のAdobe Commerceに、サードパーティアプリ（WordPress や Drupal など）をインストールすることは許可されていません。 このようなアプリケーションは、外部サーバーでホストする必要があります。
exl-id: 3abbe282-2a14-4597-8af8-da1edcbece30
feature: Cloud, Compliance, Install
source-git-commit: f11c8944b83e294b61d9547aefc9203af344041d
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# クラウドインスタンスにサードパーティのアプリケーションをインストールできますか？

いいえ。 クラウドインフラストラクチャサーバー上のAdobe Commerceに、サードパーティアプリ（WordPress や Drupal など）をインストールすることは許可されていません。 このようなアプリケーションは、外部サーバーでホストする必要があります。

## 理由

### サービス利用規約

Adobe Commerce on cloud infrastructure Edition[ 利用規約 ](https://magento.com/legal/terms/cloud-terms) は、第 18 条に以下を規定しています。

> お客様は、Adobe Commerceおよび本サービスが、本ソフトウェアに直接依存しない他のサードパーティ製ソフトウェアアプリケーションをホスティングするために使用されないことに同意します。

クラウドソリューションであるAdobeは、サーバーのセキュリティに対して完全な責任を負います。 高いセキュリティを保証するために、専用のクラウドサーバー上でAdobe Commerce アプリケーションをホストすることのみを許可します。

### PCI コンプライアンス

PCI 認定のレベル 1 のソリューションプロバイダーであるクラウドインフラストラクチャー上のAdobe Commerceは、PCI データセキュリティ標準に従い、次のことを確認する必要があります。

>...安全なシステムとアプリケーションの開発と維持
> （[PCI コンプライアンスへのAdobeアプローチ ](https://magento.com/pci-compliance) 要件 6、Maintain a Vulnerability Management Program）

Adobeでは、サードパーティ製アプリケーションの PCI 準拠を保証できないので、クラウドサーバーにそのようなアプリケーションをインストールすることはできません。

## ヒント：より良い統合のために、Commerce Marketplace拡張機能を使用する

クラウドインフラストラクチャアプリケーション上のAdobe Commerceと、外部サーバーでホストされるサードパーティのソリューションとの統合を強化するために、目的に合った [Commerce Marketplace](https://marketplace.magento.com) 拡張機能を使用することをお勧めします。
