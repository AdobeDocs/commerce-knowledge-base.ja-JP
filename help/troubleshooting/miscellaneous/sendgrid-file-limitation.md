---
title: 'Adobe Commerce Cloudの [!DNL SendGrid] ファイル制限'
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceに関する  [!DNL SendGrid]  制限事項の回避策を説明します。
feature: Deploy, Marketing Tools
role: Developer, Admin
exl-id: 48629f48-8100-4128-9211-53d947aecd49
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Adobe Commerce Cloudの [!DNL SendGrid] の制限

この記事では、クラウドインフラストラクチャー上のAdobe Commerceの [!DNL SendGrid] 制限に対する回避策をいくつか説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[&#x200B; サポート対象のすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)


## 問題

大きな添付ファイルをメールで送信しようとすると、次のログエラーが表示されます。

`/var/log/mail.log` 内

```shell
Month Date Time i-xxxxxxxxxxxxxxxxx postfix/sendmail[21408]: fatal: no-reply@xxxxxxxx.com(8080): message file too big
Month Date Time i-xxxxxxxxxxxxxxxxx postfix/sendmail[26434]: fatal: no-reply@xxxxxxxxx.com(8080): message file too big
```

`/var/log/exception.log` 内

実稼動：

`/app/<project-id>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

ステージング：

`/app/<project-id_stg>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

ステージング 2:

`/app/<project-id_stg2>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

## 原因：

[!DNL SendGrid] には、メールのシステム制限として 30 Mb のサイズがあります。 10 Mb を超える添付ファイルは使用しないことをお勧めします。 詳しくは、SendGrid ドキュメントの [&#x200B; 添付ファイルの送信 &#x200B;](https://docs.sendgrid.com/ui/sending-email/attachments-with-digioh) を参照してください。

## 回避策

* 6 MB または 10 MB を超える添付ファイルは使用しないでください。
* Adobe Commerce インスタンスでリモート SMTP サーバーを使用することを検討してください。 手順については、管理システムガイドの [&#x200B; メール通信の設定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html?lang=ja) を参照してください。
* モジュール内にファイルを保存できるようにサーバーを再設定し、メール内のファイルへのリンクを添付します。

## 関連資料

* Commerce on Cloud Infrastructure ガイドの [[!DNL SendGrid]  メールサービス &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/sendgrid.html?lang=ja)。
