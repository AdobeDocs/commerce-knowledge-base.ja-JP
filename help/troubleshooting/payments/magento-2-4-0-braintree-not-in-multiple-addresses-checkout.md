---
title: 「Adobe Commerce 2.4.0:Braintreeが複数のアドレスのチェックアウトに含まれない」
description: この記事では、複数アドレスのチェックアウトの処理にBraintree支払い方法が含まれていない、Adobe Commerce 2.4.0 の既知の問題の回避策を説明します。 この問題はAdobe Commerce 2.4.1 で修正されました。
exl-id: efde0bba-fd4a-490b-becb-856cb9ea58a5
feature: Checkout, Compliance, Orders, Payments, Shipping/Delivery
role: Developer
source-git-commit: a1046621259ea49eab74cd6ba3bba550e0c70283
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:Braintreeが複数のアドレスのチェックアウトに含まれない

この記事では、複数アドレスのチェックアウトの処理にBraintree支払い方法が含まれていない、Adobe Commerce 2.4.0 の既知の問題の回避策を説明します。 この問題はAdobe Commerce 2.4.1 で修正されました。

注意：Adobe Commerceでは、PSDのコンプライアンスを維持するために、バージョン 2.3 以降に ](https://marketplace.magento.com/paypal-module-braintree.html)0}Commerce MarketplaceBraintree拡張機能 } を使用することをお勧めします。 [拡張機能には、複数アドレスのチェックアウト機能はありません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス v2.4.0
* クラウドインフラストラクチャー上のAdobe Commerce v2.4.0

## 問題

<u> 前提条件 </u>:

コアBraintreeの統合が使用されます。

<u> 再現手順 </u>:

1. ストアフロントに移動します。
1. 顧客としてログインします。
1. 商品を買い物かごに追加します。
1. カートを開きます。
1. **買い物かごを表示して編集** を押します。
1. **複数のアドレスでチェックアウト** を押します。
1. **配送情報に移動** を押します。
1. **請求情報を続行** を押します。

<u> 期待される結果 </u>:

Braintreeはお支払い方法として利用できます。

<u> 実際の結果 </u>:

Braintreeはお支払い方法としてご利用いただけません。

## 回避策

Adobe Commerce 2.4.0 でBraintreeを使用する場合は、マルチアドレスオプションを有効にしないでください。この問題は、Adobe Commerce 2.4.1 で修正されました。

## サポートナレッジベースの関連資料

* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
