---
title: Adobe Commerce 2.4.0、2.4.1:Braintree Venmoの一部請求書を有効にする
description: この記事では、既知のAdobe Commerce 2.4.0および2.4.1の問題について説明します。この問題では、Venmoを通じてBraintreeを使用して注文した場合、部分的な請求書は使用できません。
exl-id: ef6c8aa4-a2a7-4e07-a957-23173017baf2
feature: Invoices, Orders, Payments
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 591c578b-908e-5b79-a9d3-931dfe60c24c
    internal-label: Invoices
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%
---
# Adobe Commerce 2.4.0、2.4.1:Braintree Venmoの一部請求書を有効にする

この記事では、既知のAdobe Commerce 2.4.0および2.4.1の問題について説明します。この問題では、Venmoを通じてBraintreeを使用して注文した場合、部分的な請求書は使用できません。

## 影響を受ける製品とバージョン

* Adobe Commerce on-premises 2.4.0および2.4.1
* Adobe Commerce on cloud infrastructure 2.4.0および2.4.1

## イシュー

<u>前提条件：</u>

Braintree支払い方法の設定で、**Enable Venmo through Braintree** = *Yes*&#x200B;と&#x200B;**Payment Action** = *Authorization*; **Enable Vault for Card Payments** = *No*&#x200B;を設定します。

<u>再生する手順：</u>

1. Venmo （Braintree）を支払い方法として使用して、2つ以上の商品の注文を作成します。
1. Commerce管理者で注文を開きます。
1. 注文した製品の1つに対する請求書を作成します。
1. 残りの注文された製品の請求書を作成してみてください。

<u>期待される結果：</u>

請求書が作成されました。

<u>実際の結果：</u>

次のエラーメッセージが表示されます。*「vault\_capture」コマンドが存在しません。 コマンドを確認して、もう一度やり直してください。*

## 回避策

Braintreeを使用してVenmoを通じて発注された注文の請求書を作成する際に、全額を取得します。
