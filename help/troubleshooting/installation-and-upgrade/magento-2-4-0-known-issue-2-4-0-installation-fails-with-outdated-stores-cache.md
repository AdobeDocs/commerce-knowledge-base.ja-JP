---
title: Adobe Commerce 2.4.0のインストールが古いストアキャッシュで失敗する
description: この記事では、Adobe Commerce 2.4.0のインストールが失敗し、次のエラーメッセージが表示される問題の解決策を示します。*デフォルトのweb サイトが定義されていません。 Web サイトを設定し、コンソールに表示されている。*を再試行します。
exl-id: 0680199b-7e47-4a8c-91fe-9f6c32839a0e
feature: B2B, Cache, Console, Install, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
  - id: c4af0798-d497-5e6b-8380-19812c26d00a
    internal-label: Console
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%
---
# Adobe Commerce 2.4.0のインストールが古いストアキャッシュで失敗する

この記事では、Adobe Commerce 2.4.0のインストールが失敗し、次のエラーメッセージが表示される問題の解決策について説明します。*デフォルトのweb サイトが定義されていません。 Web サイトを設定して、もう一度やり直してください。* コンソールに表示されます。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.4.0
* Adobe Commerce オンプレミス 2.4.0

## イシュー

<u>前提条件：</u>
CLI コマンドのStore モジュールのAPIに依存するサードパーティの拡張機能は、`composer.json`で必要に応じて設定されています。 これにより、Adobe Commerce 2.4.0のインストールが失敗し、エラーメッセージが表示されます。*デフォルトのweb サイトが定義されていません。 Web サイトを設定して、もう一度やり直してください。* コンソールに表示されます。

## 原因

この問題は、CLI コマンドのストアに依存しているサードパーティの拡張機能に対して発生します。 1つはAmazon Sales Channelsです。

## Solution

Adobe Commerce 2.4.0をインストールする前に、マーチャントは次のことをおこなう必要があります。

1. これらのサードパーティの拡張機能を`composer.json`から削除します。
1. 拡張機能なしでAdobe Commerceをインストールします。
1. インストール後に拡張機能を追加します。

この問題は、2.4.1 リリースのスコープで修正されます。

## サポートナレッジベースの関連リソース：

* [Adobe Commerce 2.4.0の既知の問題：Klarnaで「返金」ラベルが見つからない](/help/troubleshooting/payments/magento-2-4-0-known-issue-missing-refund-label-in-klarna.md)
* [Adobe Commerce 2.4.0、2.4.1:Braintree Venmoの請求書の一部の問題を有効にする](/help/troubleshooting/payments/magento-2-4-0-2-4-1-enable-braintree-venmo-partial-invoice-issue.md)
* [Adobe Commerce 2.4.0の既知の問題：一部の国でチェックアウト時に表示される「ローカル支払い方法を選択する」というエラーメッセージ](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0の既知の問題：Amazon Payが有効になっており、標準チェックアウトに戻る際に支払い方法が見つからない](/help/troubleshooting/payments/magento-2-4-0-known-issue-amazon-pay-no-payment-methods.md)
* [Adobe Commerce 2.4.0の既知の問題：Braintreeの支払い方法が複数のアドレスのチェックアウトに表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)

