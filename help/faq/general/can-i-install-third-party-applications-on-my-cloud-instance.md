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

Adobe Commerce on cloud infrastructure エディション [サービス利用規約](https://magento.com/legal/terms/cloud-terms) 同条第 18 条には次の条項が盛り込まれている。

> お客様は、Adobe Commerceおよび本サービスが、本ソフトウェアに直接依存しない他のサードパーティ製ソフトウェアアプリケーションをホスティングするために使用されないことに同意します。

クラウドソリューションであるAdobeは、サーバーのセキュリティに対して完全な責任を負います。 高いセキュリティを保証するために、専用のクラウドサーバー上でAdobe Commerce アプリケーションをホストすることのみを許可します。

### PCI コンプライアンス

PCI 認定のレベル 1 のソリューションプロバイダーであるクラウドインフラストラクチャー上のAdobe Commerceは、PCI データセキュリティ標準に従い、次のことを確認する必要があります。

>...安全なシステムとアプリケーションの開発と維持
> （[PCI コンプライアンスに対するAdobeアプローチ](https://magento.com/pci-compliance) 要件 6：脆弱性管理プログラムの維持）

Adobeでは、サードパーティ製アプリケーションの PCI 準拠を保証できないので、クラウドサーバーにそのようなアプリケーションをインストールすることはできません。

## ヒント：より良い統合のために、Commerce Marketplace拡張機能を使用する

クラウドインフラストラクチャアプリケーション上のAdobe Commerceと、外部サーバーでホストされるサードパーティのソリューションの統合を改善するために、 [Commerce Marketplace](https://marketplace.magento.com) 目的に合った拡張機能。
