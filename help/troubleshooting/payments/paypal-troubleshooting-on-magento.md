---
title: Adobe Commerceの PayPal トラブルシューティング
description: この記事では、PayPal、特に PayFlow Pro ソリューションを使用して支払いを処理する際の問題の解決策を提供します。 この記事のいくつかの推奨事項は明らかなように見えるかもしれません。 このナレッジベースに記載されているトラブルシューティングオプションを試して、入力したチケットにすべての情報を含めてください。 Adobe Commerceまたは PayPal サポートエンジニアは、問題を診断する際にこれらの手順を実行するように求めます。
exl-id: f0772515-8456-4f08-84b4-aeef44516f2a
feature: Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Adobe Commerceの PayPal トラブルシューティング

この記事では、PayPal、特に PayFlow Pro ソリューションを使用して支払いを処理する際の問題の解決策を提供します。 この記事のいくつかの推奨事項は明らかなように見えるかもしれません。 このナレッジベースに記載されているトラブルシューティングオプションを試して、入力したチケットにすべての情報を含めてください。 Adobe Commerceまたは PayPal サポートエンジニアは、問題を診断する際にこれらの手順を実行するように求めます。

## よくある問題

PayPal の支払いに関するほとんどの問題は同様の症状があります。支払いカードの詳細を指定し、チェックアウトに進んだ後、支払いは処理されません。 代わりに、エラーメッセージ、支払いの処理の失敗、または空白のページが表示される場合があります。

## 資格情報、暗号化キー、およびライセンスを確認します

考えられる問題：アカウントの詳細（ユーザー名、パスワード）の誤印刷、無効なアカウント、期限切れまたは指定されていないライセンス、無効な公開鍵と秘密鍵、その他の多くの側面。 これらの問題を見つけるには、支払い設定の設定を確認する必要がある場合もあります。

## Adobe Commerceと PayPal での一貫性のある設定の適用

同じ設定を適用し、Commerce管理と PayPal アカウントの両方で同じ機能を有効にしていることを確認してください。

### 設定例の問題

PayPal Express Checkout ソリューションを適用する場合、AVS/CSC 応答に基づくトランザクションは拒否する必要があります。 **PayPal マネージャー** （サービス設定/設定/セキュリティオプション）および **Commerce管理者** （ **ストア** > 設定 > **売上** > **支払い方法** ...）..
![magento_paypal_settings_2.4.1.png](assets/magento_paypal_settings_2.4.1.png)
詳しくは、次のドキュメントを参照してください。 [PayPal](https://www.paypalobjects.com/en_US/vhelp/paypalmanager_help/setup.htm) および [Adobe Commerce](/docs/commerce-admin/stores-sales/payments/paypal/paypal-express-checkout.html) を参照してください。

## 参照トランザクションを許可

PayPal の支払い方法に請求契約と参照トランザクションを含む API が含まれている場合は、設定でそれらが有効になっており、正しく設定されていることを確認してください。

### その他のトラブルシューティング

以下の記事を参照してください。

* [PayPal ゲートウェイ拒否リクエスト – 重複する請求書の問題](/help/troubleshooting/payments/paypal-gateway-rejected-request-duplicate-invoice-issue.md) サポートナレッジベースで。
* [新しいストアエンティティの増分 ID を変更](/help/how-to/general/change-increment-id-for-a-db-entity-order-invoice-credit-memo-etc-on-particular-store.md) サポートナレッジベースで。

## 高度な支払いログを収集するには、サポートにお問い合わせください

複雑な支払いの問題をトラブルシューティングするために、Adobe Commerce サポートチームから、高度な支払いログを有効にする専用パッチを適用するよう依頼される場合があります。 この場合、手順は次のようになります。

[サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) に作成します。

* 問題をできるだけ多くの詳細で指定します。
* この記事、ナレッジベース、その他のリソースから試した手順をリストします。 すべての結果を含める。
* Advanced Payment Logging パッチ（参照番号 MDVA-4352）と、パッチ適用手順をリクエストします。

「高度な支払ログ」パッチを受け取った場合：

* パッチを適用します。
* ログを収集してユーザーに添付 [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).
* Adobe Commerce サポートチームからの追加の推奨事項が表示されるまで待ちます。
