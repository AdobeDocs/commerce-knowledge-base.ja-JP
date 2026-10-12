---
title: Adobe Commerce 2.4.0：ローカルペイメントの選択でチェックアウトエラーが発生する
description: この記事では、一部の国のローカル支払い方法を選択する際にエラーメッセージが表示される、チェックアウト時のAdobe Commerceの既知の問題に対する解決策について説明します。 これは、ベルギー、イタリア、オランダ、ポーランド、スペインの国で発生します。
exl-id: de2eafb0-d03c-4ff8-9615-0f2676d95848
feature: B2B, Categories, Checkout, Orders, Payments
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
subfeature_v2:
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
    internal-label: Categories
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%
---
# Adobe Commerce 2.4.0：ローカルペイメントの選択でチェックアウトエラーが発生する

この記事では、一部の国のローカル支払い方法を選択する際にエラーメッセージが表示される、チェックアウト時のAdobe Commerceの既知の問題に対する解決策について説明します。 これは、ベルギー、イタリア、オランダ、ポーランド、スペインの国で発生します。

エラーメッセージ「*現在利用可能な支払い方法はありません。 請求先住所を更新してください。*&quot; が表示されますが、ローカルの支払い方法は引き続き表示され、正しく機能します。 恒久的な修正は、Adobe Commerce 2.4.1で利用できます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* Adobe Commerce on cloud infrastructure 2.4.0

## イシュー

<u>前提条件</u>:

* Adobe Commerce 2.4.0がインストールされます。
* ひとつの商品とひとつのカテゴリを作成。
* [Braintree支払い方法](https://developer.adobe.com/commerce/webapi/graphql/payment-methods/braintree/)を設定します。

<u>複製する手順</u>:

1. ストアフロントに移動します。
1. 買い物かごに追加する商品を選択します。
1. チェックアウトに進みます。
1. アドレスフォームに有効な住所を入力してください。
1. 「確認と支払い」ページに進みます。

<u>期待される結果</u>:

ローカルの支払い方法は、エラーメッセージなしで正常に表示されます。

<u>実際の結果</u>:

エラーメッセージ「*現在利用可能な支払い方法はありません。 請求先住所を更新してください。*&quot; が表示されますが、ローカルの支払い方法は引き続き表示され、正しく機能します。

## Solution

解決策は、表示されたエラーメッセージを無視し、すべてのローカル支払い方法が正常に機能するため、通常どおり支払いを続行することです。 この修正プログラムは、Adobe Commerce バージョン 2.4.1以降で使用できるようになりました。

## 関連トピックス

* [Adobe Commerce 2.4.0の既知の問題：Braintreeの支払い方法が複数のアドレスのチェックアウトに表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
