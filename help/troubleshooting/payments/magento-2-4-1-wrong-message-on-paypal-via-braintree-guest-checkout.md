---
title: Adobe Commerce 2.4.1:PayPal-Braintree ゲストチェックアウトの誤ったメッセージ
description: この記事では、Adobe Commerce 2.4.1の既知の問題について説明します。ゲストチェックアウトが無効になっている場合、Braintreeを通じてPayPalで注文しようとすると、情報のないエラーメッセージが表示されます。
exl-id: 758f5c57-997e-4aca-b299-9934c94fa121
feature: Checkout, Orders, Payments
role: Developer
source-git-commit: 77f41d6034f985794e5c5b89cc007a69858683b9
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Adobe Commerce 2.4.1:PayPal-Braintree ゲストチェックアウトの誤ったメッセージ

この記事では、Adobe Commerce 2.4.1の既知の問題について説明します。ゲストチェックアウトが無効になっている場合、Braintreeを通じてPayPalで注文しようとすると、情報のないエラーメッセージが表示されます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0、2.4.1
* Adobe Commerce on cloud infrastructure 2.4.0、2.4.1

## イシュー

バックエンドでゲストチェックアウトが無効になっていて、ミニカートまたはショッピングカートから「Braintree経由でPayPal」支払いオプションが選択されている場合、特定できないエラーが表示されます。

<u>前提条件</u>:

1. Commerce管理者で、**Stores** > **Configuration** > **Sales** > **Checkout**&#x200B;の下で、**Allow Guest Checkout** = *No*&#x200B;と設定します。
1. ユーザーガイドの[Braintree](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/braintree?)の説明に従って、Braintree経由でPayPalを有効にします。

<u>複製する手順</u>:

1. ゲストとして商品をカートに追加します。
1. **ミニカート**&#x200B;を選択し、**PayPalでのお支払い**&#x200B;をクリックします。
1. Paypal チェックアウトを完了すると、注文レビューページに移動します。
1. **配送方法**&#x200B;を選択します。
1. 「**注文を配置**」をクリックします。

<u>期待される結果</u>:

お客様がミニカートまたはショッピングカートページの「PayPal」ボタンをクリックすると、次のメッセージが表示されます。

<pre><code class="language-bash">To check out, please sign in with your email address.</code></pre>

Braintreeを使用せずにDirect Paypalを有効にすると、このシナリオの動作が異なります。 ゲストユーザーが支払いプロセスを続行することはできません。 ゲストユーザーがミニカートのPayPal ボタンをクリックすると、次のメッセージが表示されます。

<pre><code class="language-bash">To check out, please sign in with your email address.</code></pre>

<u>実際の結果</u>:

お客様はショッピングカートページにリダイレクトされ、次のメッセージが表示されます。

<pre><code class="language-bash">The customer email is missing. Enter and try again.</code></pre>

## 回避策

この問題の回避策は、お客様が店舗でログインできることです（ログインしたユーザーはゲストチェックアウトを使用しません）。 ゲストチェックアウトが無効になっている場所。 この問題は、Adobe Commerce バージョン 2.4.2で修正されました。

## 関連トピックス

* [Adobe Commerceの買い物かご内の商品数に関するベストプラクティス &#x200B;](https://support.magento.com/hc/en-us/articles/360048550332)をサポートナレッジベースでご覧ください。
* [注文処理チュートリアル：ステップ 1。 カート &#x200B;](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-add-items/)に商品を追加する方法については、開発者ドキュメントを参照してください
* [GraphQL チェックアウトのチュートリアル：ステップ 1。 製品をカート &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/tutorials/checkout/add-product-to-cart/)に追加する方法については、開発者ドキュメントを参照してください
