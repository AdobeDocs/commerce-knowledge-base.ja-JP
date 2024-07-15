---
title: 「頂点アドレスクレンジング：異なるアドレスは許可されません」
description: この記事では、ユーザーが Vertex の住所検証を有効にして**別**の請求先住所と配送先住所を入力しようとすると、ストアフロントはユーザーに入力させない問題の解決策について説明します。
exl-id: a481b044-3b74-4792-abc6-249a182c49e1
feature: B2B, Orders, Shipping/Delivery, Checkout
role: Developer
source-git-commit: 2bba3af8919e1db8482764b8d688f95e606c2683
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 頂点アドレスのクレンジング：異なるアドレスは許可されていません

この記事では、ユーザーが Vertex の住所検証を有効にして **別** の請求先と配送先住所を入力しようとすると、ストアフロントはユーザーに入力させない問題の解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.5-p1

## 問題

<u> 再現手順 </u>:

1. 管理者/**ストア**/**設定**/**営業**/**アドレスクレンジング** に移動します。
1. *頂点アドレスのクレンジングを使用* ドロップダウンから **有効** を選択し、**設定を保存** を選択します。
1. ゲストとしてフロントエンドに移動し、商品を買い物かごに追加します。
1. 買い物かごアイコンをクリックし **チェックアウトに進みます**。
1. アドレスフィールドに入力します。
1. 目的の **発送方法** を選択し、「**次へ**」をクリックします。
1. 「**次へ**」ボタンをもう一度クリックします。
1. 「**請求先と配送先住所****同じ**」のチェックを外し、新しい請求先住所（住所とは異なる）を入力します。
1. 「**更新**」ボタン、「**アドレスを更新** の順にクリックします。

<u> 期待される結果 </u>:

ユーザーには、異なる請求先住所と配送先住所が表示されます。

<u> 実際の結果 </u>:

ユーザーヒットが「更新」されると、請求アドレスと出荷アドレスが同じに戻ります。

## 原因：

頂点アドレスの検証に失敗しました。

## 解決策

頂点アドレスの検証を無効にするか、2.4.0 にアップグレードします。

## 関連資料

* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 の既知の問題：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する](/help/troubleshooting/storefront/magento-2-4-0-404-error-removing-rewards-points-on-multi-shipping-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 での配送ラベル作成の既知の問題](/help/troubleshooting/known-issues-patches-attached/shipping-labels-creation-known-issue-in-magento-2-4-0.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：Klarna に「返金」ラベルが見つからない](/help/troubleshooting/payments/magento-2-4-0-known-issue-missing-refund-label-in-klarna.md)
* [Adobe Commerce 2.4.0 の既知の問題：管理の「新しい注文を作成」ページに 2 つのボタンが表示されない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-create-new-order-buttons-missing.md)
* [Adobe Commerce 2.4.0 の既知の問題：Braintreeが有効な場合、Venmo の部分的な請求書の問題](/help/troubleshooting/payments/magento-2-4-0-2-4-1-enable-braintree-venmo-partial-invoice-issue.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 既知の問題：Amazon Pay が有効で、標準のチェックアウトに戻る際に支払方法が見つからない使用されます](/help/troubleshooting/payments/magento-2-4-0-known-issue-amazon-pay-no-payment-methods.md)
* [Adobe Commerce 2.4.0 の既知の問題：古いストアキャッシュを使用すると、2.4.0 のインストールが失敗します](/help/troubleshooting/installation-and-upgrade/magento-2-4-0-known-issue-2-4-0-installation-fails-with-outdated-stores-cache.md)
