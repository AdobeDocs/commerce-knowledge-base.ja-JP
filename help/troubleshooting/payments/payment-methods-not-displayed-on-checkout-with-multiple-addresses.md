---
title: 複数の住所を持つチェックアウトに支払い方法が表示されない
description: この記事では、この機能はCybersourceにのみ実装されているため、複数の配送先住所が指定されている場合、ほとんどの支払い方法がチェックアウト時に表示されないことを説明します。
exl-id: 68a9ee77-d0ef-43c5-9667-6d099b797666
feature: Checkout, Orders, Payments, Shipping/Delivery
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 04d3134c-2afb-5bd7-ac14-e19fa935e848
    internal-label: Shipping/Delivery
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
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
