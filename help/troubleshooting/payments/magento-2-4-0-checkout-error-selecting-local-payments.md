---
title: Adobe Commerce 2.4.0：現地支払いの選択でチェックアウトエラーが発生する
description: この記事では、一部の国で地域のお支払い方法を選択するとエラーメッセージが表示される、チェックアウト中のAdobe Commerceの既知の問題の解決策について説明します。 これは、ベルギー、イタリア、オランダ、ポーランド、スペインの国で発生します。
exl-id: de2eafb0-d03c-4ff8-9615-0f2676d95848
feature: B2B, Categories, Checkout, Orders, Payments
role: Developer
source-git-commit: 7705b6030d2f0877c228dae1707916ad38c9d587
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Adobe Commerce 2.4.0：現地支払いの選択でチェックアウトエラーが発生する

この記事では、一部の国で地域のお支払い方法を選択するとエラーメッセージが表示される、チェックアウト中のAdobe Commerceの既知の問題の解決策について説明します。 これは、ベルギー、イタリア、オランダ、ポーランド、スペインの国で発生します。

「*現在利用可能な支払い方法はありません。 請求先住所を更新してください。*」が表示されますが、ローカルの支払い方法は引き続き表示され、正しく機能します。 永続的な修正は、Adobe Commerce 2.4.1 で利用できるようになります。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u> 前提条件 </u>:

* Adobe Commerce 2.4.0 がインストールされています。
* 1 つの製品と 1 つのカテゴリを作成します。
* [Braintreeのお支払方法 &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/payment-methods/braintree/) を構成します。

<u> 再現手順 </u>:

1. ストアフロントに移動します。
1. 商品を選択して買い物かごに追加します。
1. チェックアウトに進みます。
1. アドレスフォームに有効なアドレスを入力します。
1. 「レビューと支払」ページに進みます。

<u> 期待される結果 </u>:

ローカルの支払い方法は、エラーメッセージなしで通常どおりに表示されます。

<u> 実際の結果 </u>:

「*現在利用可能な支払い方法はありません。 請求先住所を更新してください。*」と表示されますが、ローカルの支払い方法は引き続き表示され、正しく機能します。

## 解決策

解決策は、表示されたエラーメッセージを無視して、すべてのローカル支払い方法が正常に機能するため、通常どおり支払いを続行することです。 この修正は、Adobe Commerce バージョン 2.4.1 以降で使用可能でした。

## 関連資料

* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintreeの支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
