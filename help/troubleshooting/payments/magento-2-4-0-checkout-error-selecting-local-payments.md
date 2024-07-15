---
title: 「Adobe Commerce 2.4.0：ローカル支払いの選択でチェックアウトエラーが発生する」
description: 「この記事では、チェックアウト中にAdobe Commerceで既知の問題が発生した場合、一部の国で地域の支払い方法を選択するとエラーメッセージが表示される場合の解決策について説明します。 これは、ベルギー、イタリア、オランダ、ポーランド、スペインの国で発生します。
exl-id: de2eafb0-d03c-4ff8-9615-0f2676d95848
feature: B2B, Categories, Checkout, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '365'
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
* [Braintree支払い方法 ](https://devdocs.magento.com/guides/v2.4/graphql/payment-methods/braintree.html) を構成します。

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

* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：配送ラベルを作成すると編集ページが機能しなくなる問題が再発します](/help/troubleshooting/known-issues-patches-attached/magento-2-4-0-patch-returns-shipping-label-creation-issue.md)
* [Adobe Commerce 2.4.0 の既知の問題：顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
