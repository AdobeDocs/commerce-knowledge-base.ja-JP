---
title: Adobe Commerce 2.4.0:Braintreeが複数のアドレスのチェックアウトに含まれない
description: この記事では、複数アドレスのチェックアウトの処理にAdobe Commerceの支払い方法が含まれていない、Braintree 2.4.0 の既知の問題の回避策を説明します。 この問題はAdobe Commerce 2.4.1 で修正されました。
exl-id: efde0bba-fd4a-490b-becb-856cb9ea58a5
feature: Checkout, Compliance, Orders, Payments, Shipping/Delivery
role: Developer
source-git-commit: 05297c82b292b8ccc88018c58e991bd3a32d6ffa
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:Braintreeが複数のアドレスのチェックアウトに含まれない

この記事では、複数アドレスのチェックアウトの処理にAdobe Commerceの支払い方法が含まれていない、Braintree 2.4.0 の既知の問題の回避策を説明します。 この問題はAdobe Commerce 2.4.1 で修正されました。

注意：Adobe Commerceでは、PSDへの準拠を維持するために、バージョン 2.3 以降に [0}Commerce Marketplace Braintree拡張機能 } を使用することをお勧めします。 ](https://marketplace.magento.com/paypal-module-braintree.html)拡張機能には、複数アドレスのチェックアウト機能はありません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス v2.4.0
* クラウドインフラストラクチャー上のAdobe Commerce v2.4.0

## 問題

<u> 前提条件 </u>:

コア Braintree統合が使用されます。

<u> 再現手順 </u>:

1. ストアフロントに移動します。
1. 顧客としてログインします。
1. 商品を買い物かごに追加します。
1. カートを開きます。
1. **買い物かごを表示して編集** を押します。
1. **複数のアドレスでチェックアウト** を押します。
1. **配送情報に移動** を押します。
1. **請求情報を続行** を押します。

<u> 期待される結果 </u>:

Braintreeはお支払い方法として利用できます。

<u> 実際の結果 </u>:

Braintreeはお支払い方法としてご利用いただけません。

## 回避策

Adobe Commerce 2.4.0 でBraintreeを使用している場合は、マルチアドレスオプションを有効にしないでください。この問題は、Adobe Commerce 2.4.1 で修正されました。
