---
title: Adobe Commerce 2.4.0:Braintreeが複数アドレスのチェックアウトに含まれていない
description: この記事では、Adobe Commerce 2.4.0の既知の問題の回避策を提供します。この問題では、Braintreeの支払い方法が複数のアドレス チェックアウトの操作に含まれていません。 この問題はAdobe Commerce 2.4.1で修正されています。
exl-id: efde0bba-fd4a-490b-becb-856cb9ea58a5
feature: Checkout, Compliance, Orders, Payments, Shipping/Delivery
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 04d3134c-2afb-5bd7-ac14-e19fa935e848
    internal-label: Shipping/Delivery
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%
---
# Adobe Commerce 2.4.0:Braintreeが複数アドレスのチェックアウトに含まれていない

この記事では、Adobe Commerce 2.4.0の既知の問題の回避策を提供します。この問題では、Braintreeの支払い方法が複数のアドレス チェックアウトの操作に含まれていません。 この問題はAdobe Commerce 2.4.1で修正されています。

注意：Adobe Commerceでは、PSDのコンプライアンスを維持するために、バージョン 2.3以降では[Commerce Marketplace Braintree拡張機能](https://marketplace.magento.com/paypal-module-braintree.html)を使用することをお勧めします。 拡張機能は、マルチアドレスチェックアウト機能を提供しません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス v2.4.0
* Adobe Commerce on cloud infrastructure v2.4.0

## イシュー

<u>前提条件</u>:

Braintreeとの連携の中核が使用されます。

<u>複製する手順</u>:

1. ストアフロントに移動します。
1. 顧客としてログインします。
1. 商品をカートに追加する。
1. カートを開きます。
1. 「**カートを表示して編集**」を押します。
1. 「**複数のアドレスでチェックアウト**」を押します。
1. **配送情報に移動**&#x200B;を押します。
1. 「**請求情報を続行**」を押します。

<u>期待される結果</u>:

Braintreeは、お支払い方法としてご利用いただけます。

<u>実際の結果</u>:

Braintreeはお支払い方法としてご利用いただけません。

## 回避策

Adobe Commerce 2.4.0でBraintreeを使用している場合、マルチアドレスオプションを有効にしないでください。 この問題は、Adobe Commerce 2.4.1で修正されました。
