---
title: Adobe Commerce 2.4.1既知の問題：PayPal Braintreeでのチェックアウト時にポップアップが表示されるエラー
description: この記事では、PayPal Braintreeの支払いが使用され、複数の住所の配送が選択されている場合に、チェックアウトの請求ステップにエラーメッセージがポップアップ表示され、表示されなくなる既知のAdobe Commerce 2.4.1の問題について説明します。
exl-id: db3830b2-4885-4d89-85cd-bdcbd4b396e6
feature: Checkout, Orders, Payments
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
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%
---
# Adobe Commerce 2.4.1既知の問題：PayPal Braintreeでのチェックアウト時にポップアップが表示されるエラー

この記事では、PayPal Braintreeの支払いが使用され、複数の住所の配送が選択されている場合に、チェックアウトの請求ステップにエラーメッセージがポップアップ表示され、表示されなくなる既知のAdobe Commerce 2.4.1の問題について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.4.1
* Adobe Commerce オンプレミス 2.4.1

## イシュー

PayPal Braintreeの支払いが使用され、複数の住所の配送が選択されている場合、チェックアウトの「請求」ステップにエラーメッセージがポップアップして表示されなくなります。

<u>再生する手順：</u>

1. ストアフロントで、顧客としてログインします（管理者で有効になっている場合は、オプションでゲストチェックアウトにすることができます）。
1. 商品をカートに追加する。
1. クリックしてカートのプレビューを開きます。
1. 「**カートを表示して編集**」をクリックします。
1. 買い物かごページで、**複数のアドレスでチェックアウト**&#x200B;をクリックします。
1. 「**配送情報に移動**」をクリックし、住所を指定します。
1. 「**請求情報を続行**」をクリックします。
1. 「**PayPal Braintree**」を選択し、「**PayPal**」ボタンをクリックします。
1. ポップアップウィンドウで、**同意して支払い**&#x200B;をクリックします。

<u>期待される結果：</u>

注文はエラーなく行われます。

<u>実際の結果：</u>

注文は行われますが、エラーがあります。 *PayPal チェックアウトを初期化できませんでした。 ストア所有者*&#x200B;にお問い合わせください。  エラーは数秒間表示され、消えます。

## 修正

注文の配置がブロックされていないため、回避手順を実行する必要はありません。
