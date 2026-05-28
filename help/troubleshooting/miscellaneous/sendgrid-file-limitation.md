---
title: Adobe Commerce Cloudの[!DNL SendGrid] ファイルの制限
description: この記事では、クラウドインフラストラクチャ上のAdobe Commerceの [!DNL SendGrid] 制限に対する回避策を提供します。
feature: Deploy, Marketing Tools
role: Developer, Admin
exl-id: 48629f48-8100-4128-9211-53d947aecd49
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Adobe Commerce Cloudの[!DNL SendGrid]の制限

この記事では、Adobe Commerce on Cloud インフラストラクチャの[!DNL SendGrid]制限に対する回避策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)


## イシュー

メールに大きな添付ファイルを送信し、次のログエラーを確認しようとしました。

`/var/log/mail.log`内

```shell
Month Date Time i-xxxxxxxxxxxxxxxxx postfix/sendmail[21408]: fatal: no-reply@xxxxxxxx.com(8080): message file too big
Month Date Time i-xxxxxxxxxxxxxxxxx postfix/sendmail[26434]: fatal: no-reply@xxxxxxxxx.com(8080): message file too big
```

`/var/log/exception.log`内

本番：

`/app/<project-id>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

ステージング：

`/app/<project-id_stg>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

ステージング 2:

`/app/<project-id_stg2>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

## 原因

[!DNL SendGrid]のシステム制限は、メールのサイズが30 Mbです。 10 Mbを超える添付ファイルは使用しないことをお勧めします。 詳しくは、SendGrid ドキュメントの[添付ファイルの送信](https://docs.sendgrid.com/ui/sending-email/attachments-with-digioh)を参照してください。

## 回避策

* 6Mbまたは10Mbを超える添付ファイルは使用しないでください。
* Adobe Commerce インスタンスでのリモート SMTP サーバーの使用を検討してください。 手順については、管理者システムガイドの「[&#x200B; メール通信の設定](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html)」を参照してください。
* モジュール内にファイルを保存できるようにサーバーを再構成し、メール内のファイルへのリンクを添付します。

## 関連トピックス

* Commerce on Cloud Infrastructure ガイドの[[!DNL SendGrid] 電子メールサービス &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/sendgrid.html)。
