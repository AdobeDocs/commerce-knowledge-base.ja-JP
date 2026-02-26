---
title: Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない
description: この記事では、Klarna VBE （ベンダーバンドル拡張機能）に**払い戻し**ラベルが見つからないことに関する管理者の既知の問題の回避策を説明します。 Klarna ポータルで払い戻しを行う場合、払い戻されたバンドル製品の横に**払い戻し**ラベルが表示されません。
exl-id: f08039b2-7f8b-481e-8ec8-1659e227744f
feature: B2B, Orders, Payments
role: Developer
source-git-commit: 7705b6030d2f0877c228dae1707916ad38c9d587
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない

この記事では、Klarna VBE （Vendor Bundled Extension）に **返金** ラベルが表示されないという Admin の既知の問題の回避策を説明します。 Klarna ポータルで返金を行う場合、返金されたバンドル製品の横に **返金** ラベルが表示されません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u> 前提条件：</u>

* Klarna が有効になっています。
* バンドルされた製品が作成されます。

<u> 再現手順 </u>

1. Adobe Commerce フロントエンドに移動し、バンドルされた商品を **買い物かご** に追加します。
1. チェックアウトに移動します。
1. 消費者の情報をチェックアウトに入力し、**次へ** をクリックします。
1. **KP オプション** を選択し、**注文を配置** をクリックします。
1. **管理者**/**営業**/**注文** に移動します。
1. 注文を開きます。
1. 製品の請求書を作成します。
1. **請求書**/**請求書を選択**/**クレジット・メモ**/**払戻** （オフラインでの払戻 **ではなく）をクリックします**。
1. Klarna ポータルに移動します。
1. 注文を開きます。
1. **払い戻し** ラベルが表示されます。

<u> 期待される結果 </u>

Klarna ポータルでは、返金された商品の横に **返金** ラベルが表示されます。

<u> 実際の結果 </u>

Klarna ポータルでは、返金された商品の横に **返金** ラベルが表示されません。

## 回避策

この問題の回避策は、返金されたバンドル製品の Klarna ポータルに見つからない **返金** ラベルを無視することです。 **返金** ラベルが表示されなかったにもかかわらず、返金が発生しました。 この問題は、2020 年 Q4 のリリースを予定しているAdobe Commerce 2.4.1 で修正される予定です。

## サポートナレッジベースの関連するリーディング：

* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintreeの支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
