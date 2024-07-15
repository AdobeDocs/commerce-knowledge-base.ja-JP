---
title: 古いストアキャッシュがあると、Adobe Commerce 2.4.0 のインストールが失敗する
description: 「この記事では、Adobe Commerce 2.4.0 のインストールが失敗し、「デフォルトの web サイトが定義されていません。 Web サイトを設定して、もう一度試してください。* コンソールに表示されます。」
exl-id: 0680199b-7e47-4a8c-91fe-9f6c32839a0e
feature: B2B, Cache, Console, Install, Upgrade
role: Developer
source-git-commit: 2bba3af8919e1db8482764b8d688f95e606c2683
workflow-type: tm+mt
source-wordcount: '416'
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

この問題は、CLI コマンドでストアに依存しているサードパーティの拡張機能で発生する。 1 つ目はAmazon Sales Channelです。

## 解決策

Adobe Commerce 2.4.0 をインストールする前に、マーチャントは次の操作を行う必要があります。

1. これらのサードパーティの拡張機能を `composer.json` から削除します。
1. 拡張機能なしでAdobe Commerceをインストールします。
1. インストール後に拡張機能を追加します。

この問題は、2.4.1 リリースの範囲で修正される予定です。

## サポートナレッジベースの関連するリーディング：

* [Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない](/help/troubleshooting/payments/magento-2-4-0-known-issue-missing-refund-label-in-klarna.md)
* [Adobe Commerce 2.4.0 の既知の問題：管理の「新しい注文を作成」ページに 2 つのボタンが表示されない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-create-new-order-buttons-missing.md)
* [Adobe Commerce 2.4.0、2.4.1:BraintreeVenmo 部分請求書発行の有効化](/help/troubleshooting/payments/magento-2-4-0-2-4-1-enable-braintree-venmo-partial-invoice-issue.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 既知の問題：Amazon Pay が有効で、標準のチェックアウトに戻る際に支払方法が見つからない使用されます](/help/troubleshooting/payments/magento-2-4-0-known-issue-amazon-pay-no-payment-methods.md)
* [Adobe Commerce 2.4.0 の既知の問題：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する](/help/troubleshooting/storefront/magento-2-4-0-404-error-removing-rewards-points-on-multi-shipping-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 での配送ラベル作成の既知の問題](/help/troubleshooting/known-issues-patches-attached/shipping-labels-creation-known-issue-in-magento-2-4-0.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
