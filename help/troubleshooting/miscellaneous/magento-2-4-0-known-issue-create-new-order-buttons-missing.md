---
title: 「Adobe Commerce 2.4.0 の既知の問題：「新しい注文を作成」ボタンが表示されない」
description: この記事では、注文作成ページの 2 つのボタンが欠落しているCommerce Admin の既知の問題に対する回避策を提供します。 新規または既存の顧客に対して新しい注文を作成する際に、「SKU による製品の追加**と「製品の追加**」ボタンが見つからないので、カタログから注文に製品を追加す**ことはできません** これは、JS のバンドルが有効になっていることが原因です。 修正は、Adobe Commerce 2.4.1 で利用できるようになります。
exl-id: 24ae880e-6d74-4444-9165-2744b12af81a
feature: B2B
role: Developer
source-git-commit: a1046621259ea49eab74cd6ba3bba550e0c70283
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の既知の問題：「新規注文を作成」ボタンが表示されない

この記事では、注文作成ページの 2 つのボタンが欠落しているCommerce Admin の既知の問題に対する回避策を提供します。 新規または既存の顧客に対して新しい注文を作成する際に、「SKU による製品の追加 **と「製品の追加** ボタンが表示されず、カタログから注文に製品を追加 **できません**。 これは、JS のバンドルが有効になっていることが原因です。 修正は、Adobe Commerce 2.4.1 で利用できるようになります。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u> 再現手順 </u>

1. **顧客/すべての顧客** に移動します。
1. 顧客の **編集** リンクをクリックします。
1. 「**注文を作成** ボタンをクリックします。

<u> 期待される結果 </u>

**SKU によって製品を追加** および **製品を追加** ボタンが **新しい注文を作成** ページに表示されます。

<u> 実際の結果 </u>

**新しい注文を作成** ページに **SKU で製品を追加** ボタンと **製品を追加** ボタンが表示されません。

## 回避策

この問題の回避策は、Adobe Commerce インスタンスの JS バンドルを無効にすることです。 この問題は、2020 年 Q4 のリリースを予定しているAdobe Commerce 2.4.1 で修正される予定です。

## サポートナレッジベースの関連するリーディング

* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 の既知の問題：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する](/help/troubleshooting/storefront/magento-2-4-0-404-error-removing-rewards-points-on-multi-shipping-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
