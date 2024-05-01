---
title: 「Adobe Commerce 2.4.0:Braintreeが複数のアドレスのチェックアウトに含まれない」
description: この記事では、複数アドレスのチェックアウトの処理にBraintree支払い方法が含まれていない、Adobe Commerce 2.4.0 の既知の問題の回避策を説明します。 この問題はAdobe Commerce 2.4.1 で修正されました。
exl-id: efde0bba-fd4a-490b-becb-856cb9ea58a5
feature: Checkout, Compliance, Orders, Payments, Shipping/Delivery
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:Braintreeが複数のアドレスのチェックアウトに含まれない

この記事では、複数アドレスのチェックアウトの処理にBraintree支払い方法が含まれていない、Adobe Commerce 2.4.0 の既知の問題の回避策を説明します。 この問題はAdobe Commerce 2.4.1 で修正されました。

メモ：Adobe Commerceでは、 [Commerce MarketplaceBraintree拡張機能](https://marketplace.magento.com/paypal-module-braintree.html) （バージョン 2.3 以降でPSDのコンプライアンスを維持するために） 拡張機能には、複数アドレスのチェックアウト機能はありません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス v2.4.0
* クラウドインフラストラクチャー上のAdobe Commerce v2.4.0

## 問題

<u>前提条件</u>:

コアBraintreeの統合が使用されます。

<u>再現手順</u>:

1. ストアフロントに移動します。
1. 顧客としてログインします。
1. 商品を買い物かごに追加します。
1. カートを開きます。
1. 押す **買い物かごの表示と編集**.
1. 押す **複数のアドレスを使用してチェックアウト**.
1. 押す **配送情報に移動**.
1. 押す **請求情報の続行**.

<u>期待される結果</u>:

Braintreeはお支払い方法として利用できます。

<u>実際の結果</u>:

Braintreeはお支払い方法としてご利用いただけません。

## 回避策

Adobe Commerce 2.4.0 でBraintreeを使用する場合は、マルチアドレスオプションを有効にしないでください。この問題は、Adobe Commerce 2.4.1 で修正されました。

## サポートナレッジベースの関連資料

* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 での配送ラベル作成の既知の問題](/help/troubleshooting/known-issues-patches-attached/shipping-labels-creation-known-issue-in-magento-2-4-0.md)
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
