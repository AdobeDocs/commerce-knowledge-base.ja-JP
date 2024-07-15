---
title: PayPal ゲートウェイ拒否リクエスト – 重複する請求書の問題
description: この記事では、PayPal ゲートウェイで却下されたリクエスト（重複請求書）の問題を修正します。
exl-id: b6c4ede1-97a5-4db3-9b05-ab979cf809b3
feature: Invoices, Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# PayPal ゲートウェイ拒否リクエスト – 重複する請求書の問題

この記事では、PayPal ゲートウェイで却下されたリクエスト（重複請求書）の問題を修正します。

支払を送信する際に、重複した請求書に対してエラーが発生する場合があります。

>PayPal ゲートウェイはリクエストを拒否しました。 この請求書 ID に対する支払は既に行われています（\#10412：請求書が重複しています）

この問題は、同じ ID を持つ請求書が PayPal に複数回送信される場合に発生します。

この問題を解決するには、PayPal の支払い受け取り環境設定で、請求書 ID ごとに複数の支払いを許可します。 変更すると、PayPal は、重複した ID を持つ請求書に対しても、エラーメッセージなしで支払いを受け入れます。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス、すべてのバージョン
* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

支払いを送信すると、次のエラーメッセージが表示されます。

```
... main.CRITICAL: Exception message: PayPal gateway has rejected request. Payment has already been made for this InvoiceID (#10412: Duplicate invoice).
```

PayPal は支払いを処理して注文を完了することはできません。

## 原因：

同じ ID の請求書が PayPal に複数回送信されると、エラーメッセージが表示されます。

これは、（ローカル環境とステージング環境の両方でも）複数のAdobe Commerce サイトで同じ資格情報を使用する場合に発生する可能性があります。 次のようなシナリオが考えられます。

* 複数の店舗が PayPal に請求書を送信し、同じ請求書 ID を使用します
* 新しい店舗が、古い店舗によって以前に送信された ID を含む請求書を送信します

デフォルトでは、PayPal は同じ請求書を 2 回処理することはできません。

## 解決策

PayPal プロファイルを変更して、請求書 ID ごとに複数の支払いを許可します。 これらの変更は、PayPal を通じて行う必要があります。

1. [https://www.paypal.com](https://www.paypal.com/) でアカウントにログインします。
1. **プロファイル**/**プロファイルと設定** （右上隅）をクリックします。
1. **販売ツール** に移動します。
1. **支払いを受け取り、リスクを管理**/**支払いをブロック** に移動し、「**更新**」をクリックします。
1. **販売環境設定**、「**支払い受信環境設定**」をクリックします。
1. 「**偶発支払のブロック**」で、「**いいえ、請求書 ID ごとに複数支払を許可します** を選択します。    ![paypal_allow_multiple_payments_per_invoice_id.png](assets/paypal_allow_multiple_payments_per_invoice_id.png)
1. 一番下までスクロールして、「**保存**」をクリックします。

## 詳細情報

* PayPal デベロッパードキュメントの [ 偶発的な支払いをブロック ](https://developer.paypal.com/docs/admin/setup-account/#block-accidental-payments)。
* ユーザーガイドの PayPal でのお支払い：
   * [PayPal Express チェックアウト](/docs/commerce-admin/stores-sales/payments/paypal/paypal-express-checkout.html)
   * [その他の PayPal ソリューション](/docs/commerce-admin/stores-sales/payments/paypal/paypal.html)
* 開発者向けドキュメントでは、
   * [クラウドインフラストラクチャ上のAdobe Commerce用に PayPal 支払い方法を設定](/docs/commerce-cloud-service/user-guide/configure-store/paypal.html)
   * [Payments Integrations](https://developer.adobe.com/commerce/php/development/payments-integrations/)
