---
title: Adobe Commerce 2.4.0の既知の問題：Amazon支払い、支払い方法なし
description: この記事では、Adobe Commerce 2.4.0の既知の問題で、お客様がAmazon payを有効にした後に**標準チェックアウトに戻る**を使用すると、支払い方法が見つからない場合の解決策を紹介します。
exl-id: efd792c7-8970-4366-b9d1-4bf284ea96db
feature: B2B, Orders, Payments
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
subfeature_v2:
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%
---
# Adobe Commerce 2.4.0の既知の問題：Amazon支払い、支払い方法なし

この記事では、Adobe Commerce 2.4.0の既知の問題で、お客様がAmazon payを有効にした後に&#x200B;**標準チェックアウトに戻る**&#x200B;を使用すると、支払い方法が見つからない問題の解決策を紹介します。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure v2.3.5.p1およびv2.4.0

<u>再生する手順：</u>

1. ストアフロントに移動します。
1. カートに商品を追加して、チェックアウトに進みます。
1. Amazon Pay アカウントにログインします。
1. アドレスを選択してチェックアウトに進みます。
1. 「**標準チェックアウトに戻る**」をクリックします。
1. チェックアウトに進みます。

<u>期待される結果：</u>

支払い方法は、チェックアウトを再開した後に表示する必要があります。

<u>実際の結果：</u>

支払い方法がありません。

## Solution

解決は2.4.1に予定されています。

## サポートナレッジベースの関連リソース：

* [Adobe Commerce 2.4.0の既知の問題：一部の国でチェックアウト時に表示される「ローカル支払い方法を選択する」というエラーメッセージ](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0の既知の問題：Braintreeの支払い方法が複数のアドレスのチェックアウトに表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
