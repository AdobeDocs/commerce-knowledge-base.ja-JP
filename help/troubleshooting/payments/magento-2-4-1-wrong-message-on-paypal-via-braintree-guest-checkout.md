---
title: 「Adobe Commerce 2.4.1:PayPal Braintreeのゲストチェックアウトで間違ったメッセージが表示される」
description: この文書では、Adobe Commerce 2.4.1 の既知の問題について説明します。ゲストのチェックアウトが無効になっている場合、Braintreeを通じて PayPal で注文しようとするお客様に情報が得られないエラーメッセージが表示されます。
exl-id: 758f5c57-997e-4aca-b299-9934c94fa121
feature: Checkout, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# Adobe Commerce 2.4.1:PayPal Braintreeのゲストチェックアウトで間違ったメッセージが表示される

この文書では、Adobe Commerce 2.4.1 の既知の問題について説明します。ゲストのチェックアウトが無効になっている場合、Braintreeを通じて PayPal で注文しようとするお客様に情報が得られないエラーメッセージが表示されます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0、2.4.1
* クラウドインフラストラクチャー上のAdobe Commerce 2.4.0、2.4.1

## 問題

バックエンドからゲストのチェックアウトが無効になり、ミニ買い物かごまたは買い物かごから「Braintree決済で PayPal を使用」オプションが選択されると、特定できないエラーが表示されます。

<u> 前提条件 </u>:

1. Commerce管理者の **Stores**/**Configuration**/**Sales**/**Checkout** で、**Allow Guest Checkout**= *No* を設定します。
1. ユーザーガイドの [Braintree](https://docs.magento.com/user-guide/payment/braintree.html?) の説明に従って、Braintreeで PayPal を有効にします。

<u> 再現手順 </u>:

1. 製品をゲストとして買い物かごに追加します。
1. 「**ミニカート**」を選択し、「**PayPal で支払う**」をクリックします。
1. Paypal のチェックアウトを完了すると、注文レビューページに移動します。
1. **発送方法** を選択します。
1. **Place Order** をクリックします。

<u> 期待される結果 </u>:

顧客がミニカートまたは買い物かごページの PayPal ボタンをクリックすると、次のメッセージが顧客に表示されます。

<pre><code class="language-bash">To check out, please sign in with your email address.</code></pre>

Braintreeを使用せずにダイレクト Paypal を有効にすると、このシナリオの動作が異なります。 ゲストユーザーが支払いプロセスを続行することはできません。 ゲストユーザーがミニカートの PayPal ボタンをクリックすると、次のメッセージが表示されます。

<pre><code class="language-bash">To check out, please sign in with your email address.</code></pre>

<u> 実際の結果 </u>:

顧客は買い物かごページにリダイレクトされ、次のメッセージが表示されます。

<pre><code class="language-bash">The customer email is missing. Enter and try again.</code></pre>

## 回避策

この問題の回避策は、顧客がストアにログインできることです（ログインしたユーザーはゲストのチェックアウトを使用しません）。 ゲストのチェックアウトが無効な場所。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。

## 関連資料

* [Adobe Commerceの買い物かご内の製品数のベストプラクティス ](https://support.magento.com/hc/en-us/articles/360048550332) に関するサポートナレッジベースを参照してください。
* [ 注文処理のチュートリアル：手順 1. 開発者ドキュメントで ](https://devdocs.magento.com/guides/v2.4/rest/tutorials/orders/order-add-items.html) 買い物かごに項目を追加する
* [GraphQLのチェックアウトチュートリアル：手順 1. 開発者ドキュメントで ](https://devdocs.magento.com/guides/v2.4/graphql/tutorials/checkout/checkout-add-product-to-cart.html) 買い物かごに製品を追加する
