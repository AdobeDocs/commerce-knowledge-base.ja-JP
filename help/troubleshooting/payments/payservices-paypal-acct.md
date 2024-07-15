---
title: PayPal サンドボックスアカウントが検証されていません
description: この記事では、支払いサービスの PayPal サンドボックスアカウントが検証されず、サンドボックスのオンボーディングを完了できない理由を説明します。
exl-id: 05ce130d-6dfe-4834-bdfc-837902100118
feature: Customer Service, Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# PayPal サンドボックスアカウントが検証されていません

この記事では、支払いサービスの PayPal サンドボックスアカウントが検証されず、サンドボックスのオンボーディングを完了できない理由を説明します。

## 影響を受ける製品とバージョン

* [ 支払いサービス ](https://marketplace.magento.com/magento-payment-services.html) は、Adobe Commerce バージョン 2.4.0 から 2.4.4 と互換性を持つようになりました。

## 問題

アドビの [ オンボーディングドキュメント ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/onboard.html) では、PayPal アカウントに新規登録し、PayPal デベロッパーアカウントにログインしてから、サンドボックスアカウントを作成するように指示されています。 PayPal のオンボーディングポップアップウィンドウでオンボーディング中に新しいアカウントを作成することを選択した場合、PayPal はサンドボックスアカウントを検証できず、オンボーディングを完了できません。

<u> 再現手順 </u>:

1. [ 支払いサービスをインストール ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html) および [Commerce サービスを設定 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#configure-commerce-services) します。
1. 管理者で **支払いサービス** に移動し、[ サンドボックスのオンボーディングを開始 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/onboard.html) します。
1. 表示される PayPal オンボーディングポップアップで、オンボーディング中に（以前に作成した PayPal サンドボックスアカウントで [ ログイン ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html#test-in-sandbox-environment) ではなく、新しいビジネスアカウントを作成します。
1. PayPal のオンボーディングを正常に完了しました。
1. サンドボックスの支払いが保留中であり、オンボーディングを完了するには PayPal でメールアドレスを確認する必要があるという通知が管理者に表示されます。

   PayPal がメールアドレスを確認できなかったので、確認メールが届きませんでした。

## 原因：

PayPal アカウントの前にサンドボックスアカウントを作成すると、PayPal はサンドボックスアカウントを検証できず、サンドボックスオンボーディング（つまり、支払いを受け入れたり、サンドボックスモードをテストしたりできません）を完了できません。

## 解決策

1. [PayPal 開発者 ](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account) ポータルで作成されたサンドボックスアカウントを使用します。
1. [ サンドボックスをリセット ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html#test-in-sandbox-environment) をクリックし、サンドボックスのオンボーディングを再開します。
1. [ アカウントの問題を軽減してオンボーディングを再開し、支払いを受け入れることができない場合は、サポートにお問い合わせください ](mailto:payment-services-support@adobe.com)。
