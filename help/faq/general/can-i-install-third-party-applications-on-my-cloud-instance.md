---
title: クラウドインスタンスにサードパーティアプリケーションをインストールできますか？
description: いいえ。 クラウドインフラストラクチャサーバー上のAdobe Commerceにサードパーティ製のアプリケーション（WordPressやDrupalなど）をインストールすることは許可されていません。 このようなアプリケーションは、外部サーバー上でホストする必要があります。
exl-id: 3abbe282-2a14-4597-8af8-da1edcbece30
feature: Cloud, Compliance, Install
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%
---
# クラウドインスタンスにサードパーティアプリケーションをインストールできますか？

いいえ。 クラウドインフラストラクチャサーバー上のAdobe Commerceにサードパーティ製のアプリケーション（WordPressやDrupalなど）をインストールすることは許可されていません。 このようなアプリケーションは、外部サーバー上でホストする必要があります。

## 理由

### SLA

Adobe Commerce on cloud infrastructure Edition [ サービス利用規約](https://magento.com/legal/terms/cloud-terms)には、その第18条に次のように記載されています。

> お客様は、Adobe Commerceおよび本サービスが、本ソフトウェアに直接依存しない他のサードパーティ製ソフトウェアアプリケーションをホストするために使用されないことに同意するものとします。

Adobeはクラウドソリューションであるため、サーバーのセキュリティに対する全責任を負います。 高いセキュリティを保証するために、Adobe Commerce アプリケーションは専用のクラウドサーバーでのみホスティングできます。

### PCI認定

PCI認定を受けたレベル 1のソリューションプロバイダーであるAdobe Commerce on cloud インフラストラクチャは、PCI データセキュリティ標準に準拠し、次のことを確実に実行する必要があります。

>...安全なシステムとアプリケーションの開発と維持
> （[AdobeのPCI コンプライアンスに関する取り組み](https://magento.com/pci-compliance)要件6、脆弱性管理プログラムの維持）

Adobeは、サードパーティアプリケーションのPCI認定を保証できないため、そのようなアプリケーションをクラウドサーバーにインストールすることは許可されていません。

## ヒント：より優れた統合を行うには、Commerce Marketplaceの拡張機能を使用します

外部サーバー上でホストされているサードパーティ製ソリューションとAdobe Commerce オンクラウド インフラストラクチャ アプリケーションの統合を強化するには、目的に合わせて[Commerce Marketplace](https://marketplace.magento.com)拡張機能を使用することをお勧めします。
