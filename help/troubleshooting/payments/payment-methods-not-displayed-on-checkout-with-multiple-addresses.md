---
title: 複数の住所を持つチェックアウトに支払い方法が表示されない
description: この記事では、この機能はCybersourceにのみ実装されているため、複数の配送先住所が指定されている場合、ほとんどの支払い方法がチェックアウト時に表示されないことを説明します。
exl-id: 68a9ee77-d0ef-43c5-9667-6d099b797666
feature: Checkout, Orders, Payments, Shipping/Delivery
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 複数の住所を持つチェックアウトに支払い方法が表示されない

この記事では、この機能はCybersourceにのみ実装されているため、複数の配送先住所が指定されている場合、ほとんどの支払い方法がチェックアウト時に表示されないことを説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.x.x
* Adobe Commerce on cloud infrastructure 2.x.x

>[!NOTE]
>
>Adobe Commerce Cybersourceのコア決済インテグレーションは2.3.3以降で廃止され、2.4.0で完全に削除されます。 代わりに、Marketplaceの[公式拡張機能](https://marketplace.magento.com/cybersource-global-payment-management.html)を使用してください。

## イシュー

<u>前提条件</u>: Commerce管理者で、PayPalとCybersourceの支払い方法を有効にして設定し、ストアのマルチシッピングを有効にします。

<u>複製する手順</u>:

1. ストアフロントで、複数の商品をカートに追加します。
1. ショッピングカートのページへ。
1. 「**複数のアドレスでチェックアウト**」をクリックします。
1. ログインするか、アカウントを作成します。
1. 「複数の住所への配送」ページのアドレス間で商品を分割します。
1. 「**配送情報に移動**」をクリックします。
1. 各配送の配送方法を選択します。
1. 「**請求情報を続行**」をクリックします。

<u>期待される結果</u>：支払いオプションとしてPayPalおよびCybersourceを利用できます。

<u>実際の結果</u>: サイバーソースのみが使用可能な支払いオプションとして表示されます。

## 原因

現在、Cybersourceは、バージョン 2.2.4以降、マルチシッピングチェックアウトでサポートされている唯一のライブ支払い方法です。 マルチシッピングのサポートは、各支払い方法ごとに1つずつ構築される可能性があります。 現時点では、正確な日付やリリース番号を提供することはできません。
