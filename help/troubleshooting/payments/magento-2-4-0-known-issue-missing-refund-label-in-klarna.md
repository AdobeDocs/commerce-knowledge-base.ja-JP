---
title: 「Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない」
description: この記事では、Klarna VBE （ベンダーバンドル拡張機能）に**払い戻し**ラベルが見つからないことに関する管理者の既知の問題の回避策を説明します。 Klarna ポータルで払い戻しを行う場合、払い戻されたバンドル製品の横に**払い戻し**ラベルが表示されません。
exl-id: f08039b2-7f8b-481e-8ec8-1659e227744f
feature: B2B, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない

この記事では、が見つからないという管理者の既知の問題に対する回避策を説明します **払戻** Klarna VBE （ベンダーバンドル拡張機能）のラベル。 Klarna ポータルで払い戻しを行う場合、 **払戻** 払い戻されたバンドル製品の横にラベルが表示されない。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u>前提条件：</u>

* Klarna が有効になっています。
* バンドルされた製品が作成されます。

<u>再現手順</u>

1. Adobe Commerce フロントエンドに移動し、バンドル製品をに追加します **カート**.
1. チェックアウトに移動します。
1. 消費者の情報をチェックアウトに入力してクリックします **次**.
1. を選択 **KP オプション** をクリックして、 **注文する**.
1. に移動 **Admin** > **売上** > **注文件数**.
1. 注文を開きます。
1. 製品の請求書を作成します。
1. に移動 **請求書** > **請求書を選択** > クリック **クレジット メモ** > クリック **払戻** （ではない **オフラインでの払い戻し**）に設定します。
1. Klarna ポータルに移動します。
1. 注文を開きます。
1. この **払戻** ラベルが存在する。

<u>期待される結果</u>

Klarna ポータル上で、 **払戻** 払い戻された商品の横にラベルが表示されます。

<u>実際の結果</u>

Klarna ポータル上で、 **払戻** 払い戻された商品の横にラベルが表示されません。

## 回避策

この問題の回避策は、が見つからないを無視することです **払戻** 返金されたバンドル製品に関する Klarna ポータルのラベル。 払い戻しは発生しましたが、 **払戻** ラベルが表示されませんでした。 この問題は、2020 年 Q4 のリリースを予定しているAdobe Commerce 2.4.1 で修正される予定です。

## サポートナレッジベースの関連するリーディング：

* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 の既知の問題：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する](/help/troubleshooting/storefront/magento-2-4-0-404-error-removing-rewards-points-on-multi-shipping-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 での配送ラベル作成の既知の問題](/help/troubleshooting/known-issues-patches-attached/shipping-labels-creation-known-issue-in-magento-2-4-0.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
