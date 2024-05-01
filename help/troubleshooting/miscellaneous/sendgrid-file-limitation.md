---
title: '''[!DNL SendGrid] Adobe Commerce Cloudのファイル制限'
description: この記事では、の回避策を説明します  [!DNL SendGrid] クラウドインフラストラクチャー上のAdobe Commerceの制限事項
feature: Deploy, Marketing Tools
role: Developer, Admin
exl-id: 48629f48-8100-4128-9211-53d947aecd49
source-git-commit: a28257f55abf21cddec9b415e7e8858df33647be
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# [!DNL SendGrid] Adobe Commerce Cloudの制限

この記事では、次の問題の回避策を提供します [!DNL SendGrid] クラウドインフラストラクチャー上のAdobe Commerceの制限事項

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)


## 問題

大きな添付ファイルをメールで送信しようとすると、次のログエラーが表示されます。

対象： `/var/log/mail.log`

```shell
Month Date Time i-xxxxxxxxxxxxxxxxx postfix/sendmail[21408]: fatal: no-reply@xxxxxxxx.com(8080): message file too big
Month Date Time i-xxxxxxxxxxxxxxxxx postfix/sendmail[26434]: fatal: no-reply@xxxxxxxxx.com(8080): message file too big
```

対象： `/var/log/exception.log`

実稼動：

`/app/<project-id>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

ステージング：

`/app/<project-id_stg>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

ステージング 2:

`/app/<project-id_stg2>/vendor/laminas/laminas-mail/src/Transport/Sendmail.php:313`

## 原因：

[!DNL SendGrid] には、メールのシステム制限として 30 Mb サイズがあります。 10 Mb を超える添付ファイルは使用しないことをお勧めします。 参照： [添付ファイルの送信](https://docs.sendgrid.com/ui/sending-email/attachments-with-digioh) 詳しくは、SendGrid のドキュメントを参照してください。

## 回避策

* 6 MB または 10 MB を超える添付ファイルは使用しないでください。
* Adobe Commerce インスタンスでリモート SMTP サーバーを使用することを検討してください。 手順については、次を参照してください [メール通信を設定する](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html) アドビの管理システムガイドをご覧ください。
* モジュール内にファイルを保存できるようにサーバーを再設定し、メール内のファイルへのリンクを添付します。

## 関連資料

* [[!DNL SendGrid] メールサービス](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/sendgrid.html) クラウドインフラストラクチャーに関するCommerceのガイドを参照してください。
