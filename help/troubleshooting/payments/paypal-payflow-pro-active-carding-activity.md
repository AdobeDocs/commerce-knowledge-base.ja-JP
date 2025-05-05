---
title: PayPal Payflow Pro アクティブなカード処理アクティビティ
description: 更新日：2019 年 4 月 2 日（PT）
exl-id: 9fe73788-5b67-445a-9b0d-86489125d271
feature: Cache, Orders, Payments
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# PayPal Payflow Pro アクティブなカード処理アクティビティ

更新日：2019 年 4 月 2 日（PT）

Adobe Commerceの PayPal Payflow Pro との連携は、カードのアクティビティによってアクティブにターゲットされており、攻撃者はカードの有効性を確認するために盗まれたクレジットカードで数百ドルの取引を試みます。

このアクティビティは現在、Magento Open SourceおよびCommerce（オンプレミスおよびクラウド）用にAdobe Commerce 2.1.x、2.2.x、2.3.x に含まれていた Payflow Pro 統合のバージョンを対象としています。 カード処理アクティビティは、Payflow Pro が買い物かごに統合される方法に固有のものです。

>[!NOTE]
>
>これらの問題を解決するために、Payflow Pro のチェックアウトフォームにGoogle reCAPTCHA または CAPTCHA を追加する新しい Composer パッケージを提供しました。 これらのパッケージを、すべてのAdobe Commerceのバージョンとエディションにインストールすることをお勧めします。

この問題は、次のAdobe Commerceのバージョンに影響します。

* Adobe Commerce オンプレミス v2.1.x、2.2.x、2.3.x
* クラウドインフラストラクチャー上のAdobe Commerce v2.1.x、2.2.x、2.3.x

## 問題

これらの攻撃の症状には、次のものがあります。

* PayPal Payflow Pro アカウントには、何百件もの不正な取引が特定されたことが表示されます
* PayPal は、不正取引の発生により Payflow Pro アカウントを停止し、多額の手数料を請求する場合があります

## 解決策

これらの攻撃から保護するために、Payflow Pro のチェックアウトフォームにGoogle reCAPTCHA （推奨）または CAPTCHA を追加することをお勧めします。 これには、Composer パッケージのインストールと、Commerce Admin でのGoogle reCAPTCHA または CAPTCHA の設定が含まれます。

### パッケージのインストール

Adobeは、Google reCAPTCHA や CAPTCHA を Payflow Pro チェックアウトフォームに追加するための 2 つのパッケージオプションを作成しました。 これらのパッケージの 1 つをインストールすると、現在のインストールが更新され、Payflow Pro チェックアウトフォームにこのセキュリティを強化するのに役立つオプションが追加されます。

これらのパッケージは、次のAdobe Commerce デプロイメントおよびバージョンと互換性があります。

Adobe Commerce（すべてのデプロイメント方法）およびMagento Open Source 2.1.x、2.2.x、2.3.x

インストールには、Adobe Commerce インスタンスへの CLI コマンドが必要です。 開発者の支援が必要になる場合があります。

>[!NOTE]
>
>関連する Payflow Pro チェックアウトフォームのアップデートをインストールする以外に、Google reCAPTCHA をインストールして設定することをお勧めします。 このオプションを選択すると、非表示のチェックと複数の設定オプションが提供されます。

#### Google reCAPTCHA のインストールとフォームのアップデートのチェックアウト

`magento/module-paypal-recaptcha` パッケージには、Google reCAPTCHA および Payflow Pro 支払いフォームのアップデートとの統合が含まれています。 reCAPTCHA モジュールをインストールして設定している場合でも、このパッケージをインストールすることをお勧めします。

次のコマンドを実行してインストールします。

**Adobe Commerce オンプレミスの場合：**

```bash
composer require magento/module-paypal-recaptcha
bin/magento module:enable Magento_PaypalReCaptcha
bin/magento setup:upgrade
bin/magento cache:clean
```

**クラウドインフラストラクチャー上のAdobe Commerceの場合：**

1. 次のコマンドを実行します。

   ```bash
   composer require magento/module-paypal-recaptcha
   ```

1. 変更をコミットしてプッシュします。

   ```bash
   git add -A && git commit -m "Install Google reCAPTCHA"    git push origin %branch_name%
   ```

1. デプロイメントが完了するまで待ちます。

#### CAPTCHA のチェックアウトフォームのアップデートのインストール

`magento/module-paypal-captcha` パッケージには、ネイティブのAdobe Commerce CAPTCHA モジュールとの統合が含まれています。

次のコマンドを実行してインストールします。

**Adobe Commerce オンプレミスの場合：**

```bash
composer require magento/module-paypal-captcha
bin/magento module:enable Magento_PaypalCaptcha
bin/magento setup:upgrade
bin/magento cache:clean
```

**クラウドインフラストラクチャー上のAdobe Commerceの場合：**

1. 次のコマンドを実行します。

   ```bash
   composer require magento/module-paypal-captcha
   ```

1. 変更をコミットしてプッシュします。

   ```bash
   git add -A && git commit -m "Install CAPTCHA"    git push origin %branch_name%
   ```

1. デプロイメントが完了するまで待ちます。

### Google reCAPTCHA または CAPTCHA の設定

パッケージのインストール後、次のドキュメントに示すように、Google reCAPTCHA （推奨）または CAPTCHA を設定します。

* ユーザーガイドの [Google reCAPTCHA](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/captcha/security-google-recaptcha)。
* ユーザーガイドの [CAPTCHA](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/captcha/security-captcha)。

新しいチェックアウトフォームオプションは次のとおりです。

* Google reCAPTCHA:PayPal Payflow Pro 支払いフォームでの使用
* CAPTCHA:Payflow Pro

## PayPal サポートおよび連絡先

不正防止サービスの詳細については、PayPal Payflow マーチャントサポートにお問い合わせください。 PayPal サポートチームに対して [Basic Fraud Protection Services](https://developer.paypal.com/api/nvp-soap/payflow/fraud-protection/) フィルターを有効にして、支払いに関して可能な限り厳密な制御を提供するようにリクエストできます。これにより、不正な取引につながる可能性のある支払いを自動的に拒否し、通常は問題とならない支払いを受け入れることができます。 PayPal 不正防止サービスフィルターを有効にすると、取引が決済されるまで最大 2 時間かかることがあります。

>[!NOTE]
>
>詳しくは、PayPal の KB [ 「Adobeから Payflow Pro との連携について連絡がありました。 どうすれば良いですか？」 ](https://www.paypal.com/us/smarthelp/article/ts2242)。

**PayPal Payflow マーチャントサポートの詳細**

Payflow マーチャントサポートの営業時間は、月曜日から金曜日の午前 7:00～午後 8:00 （中央標準時）です。 電話またはメールでアカウントのサポートを受ける場合は、Payflow マーチャントサポートにお問い合わせください。

* 電話：1-888-883-9770 （プロンプト 2 を選択）
* 海外のお客様：1-408-967-0191
* メール：[payflow-support@paypal.com](mailto:payflow-support@paypal.com)

オーストラリアのサポート

* 月曜日～金曜日の午前 8:00～午後 7:00 （アフリカ時間）
* 電話：+61 2 8288 0198
* メール：[gateway-ausupport@paypal.com](mailto:gateway-ausupport@paypal.com)
