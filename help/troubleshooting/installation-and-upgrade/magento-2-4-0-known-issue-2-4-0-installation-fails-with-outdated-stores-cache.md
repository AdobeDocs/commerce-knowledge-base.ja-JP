---
title: 古いストアキャッシュがあると、Adobe Commerce 2.4.0 のインストールが失敗する
description: この記事では、Adobe Commerce 2.4.0 のインストールが失敗し、「デフォルトの web サイトが定義されていません。 Web サイトを設定して、もう一度試してください。*がコンソールに表示されます。
exl-id: 0680199b-7e47-4a8c-91fe-9f6c32839a0e
feature: B2B, Cache, Console, Install, Upgrade
role: Developer
source-git-commit: 05297c82b292b8ccc88018c58e991bd3a32d6ffa
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 古いストアキャッシュがあると、Adobe Commerce 2.4.0 のインストールが失敗する

ここでは、Adobe Commerce 2.4.0 のインストールが失敗して「*デフォルトの web サイトが定義されていません。 Web サイトを設定して、もう一度試してください。コ* ソールに表示されます。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## 問題

<u> 前提条件：</u>
CLI コマンドの格納モジュールの API への依存関係を持つサードパーティ製拡張機能は、`composer.json` で必要に応じて設定されます。 これにより、Adobe Commerce 2.4.0 のインストールが失敗し、「*デフォルトの web サイトが定義されていません。 Web サイトを設定して、もう一度試してください。コ* ソールに表示されます。

## 原因：

この問題は、CLI コマンドでストアに依存しているサードパーティの拡張機能で発生する。 1 つは、Amazonの販売チャネルです。

## 解決策

Adobe Commerce 2.4.0 をインストールする前に、マーチャントは次の操作を行う必要があります。

1. これらのサードパーティの拡張機能を `composer.json` から削除します。
1. 拡張機能なしでAdobe Commerceをインストールします。
1. インストール後に拡張機能を追加します。

この問題は、2.4.1 リリースの範囲で修正される予定です。

## サポートナレッジベースの関連するリーディング：

* [Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない](/help/troubleshooting/payments/magento-2-4-0-known-issue-missing-refund-label-in-klarna.md)
* [Adobe Commerce 2.4.0、2.4.1: Braintree Venmo 部分請求書発行の有効化](/help/troubleshooting/payments/magento-2-4-0-2-4-1-enable-braintree-venmo-partial-invoice-issue.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 既知の問題：Amazon Pay が有効で、標準のチェックアウトに戻る際に支払方法が見つからない使用されます](/help/troubleshooting/payments/magento-2-4-0-known-issue-amazon-pay-no-payment-methods.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintreeの支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)

