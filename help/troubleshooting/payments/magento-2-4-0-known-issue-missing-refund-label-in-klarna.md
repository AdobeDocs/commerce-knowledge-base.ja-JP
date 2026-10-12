---
title: Adobe Commerce 2.4.0の既知の問題：Klarnaで「返金」ラベルが見つからない
description: この記事では、Klarna VBE （Vendor Bundled Extension）で見つからない**Refund** ラベルに関する、Adminの既知の問題の回避策について説明します。 Klarna ポータルで払い戻しを行うと、払い戻された同梱商品の横に**払い戻し** ラベルが表示されません。
exl-id: f08039b2-7f8b-481e-8ec8-1659e227744f
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
source-wordcount: '332'
ht-degree: 0%
---
# Adobe Commerce 2.4.0の既知の問題：Klarnaで「返金」ラベルが見つからない

この記事では、Klarna VBE （Vendor Bundled Extension）で&#x200B;**返金** ラベルが見つからない場合の管理者の既知の問題の回避策について説明します。 Klarna ポータルで払い戻しを行うと、払い戻された同梱商品の横に&#x200B;**払い戻し** ラベルが表示されません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* Adobe Commerce on cloud infrastructure 2.4.0

## イシュー

<u>前提条件：</u>

* Klarnaが有効になっています。
* バンドル製品が作成されます。

<u>複製する手順</u>

1. Adobe Commerce フロントエンドに移動し、**買い物かご**&#x200B;にバンドル商品を追加します。
1. Checkoutに移動します。
1. チェックアウトに消費者情報を入力し、**次へ**&#x200B;をクリックします。
1. **KP オプション**&#x200B;を選択し、**注文を配置**&#x200B;をクリックします。
1. **管理者** > **販売** > **注文**&#x200B;に移動します。
1. 注文を開きます。
1. 製品の請求書を作成します。
1. **請求書** > **請求書を選択** > **クレジットメモ**&#x200B;をクリック > **返金**&#x200B;をクリックします（**オフライン返金**&#x200B;ではありません）。
1. Klarna Portalにアクセスします。
1. 注文を開きます。
1. **返金** ラベルが存在します。

<u>期待される結果</u>

Klarna ポータルでは、返金された商品の横に「**返金**」ラベルが表示されます。

<u>実際の結果</u>

Klarna ポータルでは、返金された商品の横に&#x200B;**返金** ラベルが表示されません。

## 回避策

この問題の回避策は、Klarna ポータルで見つからない&#x200B;**返金** ラベルを無視して、返金された同梱製品を対象にすることです。 **返金** ラベルが表示されなかったにもかかわらず、返金が発生しました。 この問題は、2020年第4四半期にリリース予定のAdobe Commerce 2.4.1で修正される予定です。

## サポートナレッジベースの関連リソース：

* [Adobe Commerce 2.4.0の既知の問題：Braintreeの支払い方法が複数のアドレスのチェックアウトに表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0の既知の問題：一部の国でチェックアウト時に表示される「ローカル支払い方法を選択する」というエラーメッセージ](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
