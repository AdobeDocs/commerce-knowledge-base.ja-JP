---
title: PayPal サンドボックスアカウントが検証されていません
description: この記事では、支払いサービスの PayPal サンドボックスアカウントが検証されず、サンドボックスのオンボーディングを完了できない理由を説明します。
exl-id: 05ce130d-6dfe-4834-bdfc-837902100118
feature: Customer Service, Orders, Payments
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# PayPal サンドボックスアカウントが検証されていません

この記事では、支払いサービスの PayPal サンドボックスアカウントが検証されず、サンドボックスのオンボーディングを完了できない理由を説明します。

## 影響を受ける製品とバージョン

* [支払いサービス](https://marketplace.magento.com/magento-payment-services.html) は、Adobe Commerce バージョン 2.4.0～2.4.4 と互換性を持つようになりました。

## 問題

当社の [オンボーディングドキュメント](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/onboard.html) は、PayPal アカウントに新規登録し、PayPal デベロッパーアカウントにログインしてから、サンドボックスアカウントを作成するように指示します。 PayPal のオンボーディングポップアップウィンドウでオンボーディング中に新しいアカウントを作成することを選択した場合、PayPal はサンドボックスアカウントを検証できず、オンボーディングを完了できません。

<u>再現手順</u>:

1. あなた [支払いサービスのインストール](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html) および [Commerce サービスの設定](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#configure-commerce-services).
1. 次に移動します **支払いサービス** 管理画面および [サンドボックスのオンボーディングを開始](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/onboard.html).
1. 表示される PayPal オンボーディングポップアップで、（の代わりに）新しいビジネスアカウントを作成します。 [以前に作成した PayPal サンドボックスアカウントを使用したログイン](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html#test-in-sandbox-environment) オンボーディング中に。
1. PayPal のオンボーディングを正常に完了しました。
1. サンドボックスの支払いが保留中であり、オンボーディングを完了するには PayPal でメールアドレスを確認する必要があるという通知が管理者に表示されます。

   PayPal がメールアドレスを確認できなかったので、確認メールが届きませんでした。

## 原因：

PayPal アカウントの前にサンドボックスアカウントを作成すると、PayPal はサンドボックスアカウントを検証できず、サンドボックスオンボーディング（つまり、支払いを受け入れたり、サンドボックスモードをテストしたりできません）を完了できません。

## 解決策

1. で作成されたサンドボックスアカウントを使用 [PayPal 開発者](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account) ポータル。
1. クリック [サンドボックスをリセット](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html#test-in-sandbox-environment) を選択し、サンドボックスのオンボーディングを再開します。
1. [サポートに連絡](mailto:payment-services-support@adobe.com) アカウントの問題を軽減できず、オンボーディングを再開して支払いを受け入れることができない場合。
