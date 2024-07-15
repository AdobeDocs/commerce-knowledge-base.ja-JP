---
title: 'Adobe Commerce 2.4.0:「選択内容を買い物かごに追加」が機能しない'
description: この記事では、顧客の買い物かごを管理する際にCommerce管理者で発生する、壊れたボタンの既知の問題に対する回避策を説明します。 選択した製品を顧客の買い物かごに追加しようとすると、セクションの下部にある**選択を自分の買い物かごに追加**ボタンが機能しません。 この問題は、2 つの**買い物かごに選択項目を追加**ボタンを含む管理パネルページで発生します。 永続的な修正は、Adobe Commerce 2.4.1 で利用できるようになります。
exl-id: b0830ec2-2aea-4afb-8d02-e9c8f54283be
feature: Orders, Shopping Cart
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:「買い物かごに選択項目を追加」が機能しない

この記事では、顧客の買い物かごを管理する際にCommerce管理者で発生する、壊れたボタンの既知の問題に対する回避策を説明します。 選択した製品を顧客の買い物かごに追加しようとすると、セクションの下部にある **選択を自分の買い物かごに追加** ボタンが機能しません。 この問題は、2 つの **買い物かごに選択項目を追加** ボタンを含む管理パネルページで発生します。 永続的な修正は、Adobe Commerce 2.4.1 で利用できるようになります。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.0 （すべてのデプロイメント方法）

## 問題

<u> 再現手順 </u>

1. 「買い物かごに選択項目を追加 **ボタンを 2 つ含む管理パネルページに移動し** す。
1. 商品を選択して買い物かごに追加します。
1. セクションの下部にある「**選択内容をカートに追加**」ボタンをクリックします。

<u> 期待される結果 </u>

すべての選択内容が期待どおりに買い物かごに追加されます。

<u> 実際の結果 </u>

Adobe Commerceが選択内容を買い物かごに追加しません。

## 解決策

ページ上部の **選択をカートに追加** ボタンは引き続き機能します。 この問題は、第 4 四半期 1 にリリースされる予定のAdobe Commerce バージョン 2.4.1 で修正される予定です。

## 関連資料

* ユーザーガイドの [MerchDocs](https://docs.magento.com/user-guide/sales/shopping-assisted-cart-manage.html) 買い物かごの管理。
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示されます ](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md) アドビのサポートナレッジベースを参照してください。
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しません ](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md) アドビのサポートナレッジベースを参照してください。
* [Adobe Commerce 2.4.0 既知の問題：Braintreeのお支払い方法が複数アドレスのチェックアウトに表示されません ](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md) アドビのサポートナレッジベースを参照してください。
