---
title: 'Adobe Commerce 2.4.0、2.4.1:BraintreeVenmo 部分請求の有効化'
description: ここでは、Adobe Commerce 2.4.0 および 2.4.1 の既知の問題について説明します。この問題では、Venmo を通じてBraintreeを使用して注文した場合に、部分的な請求を利用できません。
exl-id: ef6c8aa4-a2a7-4e07-a957-23173017baf2
feature: Invoices, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Adobe Commerce 2.4.0、2.4.1:BraintreeVenmo 部分請求書の有効化

ここでは、Adobe Commerce 2.4.0 および 2.4.1 の既知の問題について説明します。この問題では、Venmo を通じてBraintreeを使用して注文した場合に、部分的な請求を利用できません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0 および 2.4.1
* クラウドインフラストラクチャー 2.4.0 および 2.4.1 上のAdobe Commerce

## 問題

<u>前提条件：</u>

Braintree支払方法コンフィギュレーションで、を設定します **Braintreeによる Venmo の有効化** = *はい* （を使用） **支払いアクション** = *認証*; **カード支払に対する Vault の有効化** = *不可*.

<u>再現手順：</u>

1. Venmo （Braintree）を支払い方法として使用して、2 つ以上の商品の注文を作成します。
1. Commerce Admin で注文を開きます。
1. 注文した製品の 1 つに対して請求書を作成します。
1. 残りの注文済み製品については請求書を作成してみます。

<u>期待される結果：</u>

請求書が作成されました。

<u>実際の結果：</u>

次のエラーメッセージが表示されます。 *「vault\_capture」コマンドが存在しません。 コマンドを確認し、もう一度試してください。*

## 回避策

Venmo を通じてBraintreeを使用して注文の請求書を作成する際に、合計金額をキャプチャします。
