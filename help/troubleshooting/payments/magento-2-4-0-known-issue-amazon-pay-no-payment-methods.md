---
title: Adobe Commerce 2.4.0 既知の問題：Amazon pay、支払い方法なし
description: この記事では、Adobe Commerce支払いを有効にした後に、お客様が**標準チェックアウトに戻る**を使用した際に支払い方法が見つからない、Amazon 2.4.0 の既知の問題に対するソリューションを提供します。
exl-id: efd792c7-8970-4366-b9d1-4bf284ea96db
feature: B2B, Orders, Payments
role: Developer
source-git-commit: 60f68b9edabd13a69e84705b85d84fd10ee6e2be
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 既知の問題：Amazon pay、支払い方法なし

この記事では、Adobe Commerce支払いを有効にした後に、お客様が **標準チェックアウトに戻る** を使用した際に支払い方法が見つからない、Amazon 2.4.0 の既知の問題に対するソリューションを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure v2.3.5.p1 および v2.4.0

<u> 再現手順：</u>

1. ストアフロントに移動します。
1. カートに商品を追加し、チェックアウトに進みます。
1. Amazon Pay アカウントにログインします。
1. 住所を選択し、チェックアウトに進みます。
1. 「**標準チェックアウトに戻る**」をクリックします。
1. チェックアウトに進みます。

<u> 期待される結果：</u>

チェックアウトを再開すると、支払い方法が表示されます。

<u> 実績：</u>

支払い方法がありません。

## 解決策

解決は 2.4.1 で予定されています。

## サポートナレッジベースの関連するリーディング：

* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintreeの支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
