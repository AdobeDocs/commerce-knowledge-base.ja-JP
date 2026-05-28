---
title: アカウント権限とアクセスキーに関連するデプロイメントの問題
description: この記事では、アクセスキーの所有権の競合によって引き起こされるクラウドインフラストラクチャへのAdobe Commerceのデプロイに関する問題の解決策を提供します。
exl-id: e8d72ebe-453f-4d18-a25e-c76e685aa667
feature: Deploy, Roles/Permissions
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# アカウント権限とアクセスキーに関連するデプロイメントの問題

この記事では、アクセスキーの所有権の競合によって引き起こされるクラウドインフラストラクチャへのAdobe Commerceのデプロイに関する問題の解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure （サポートされているすべてのバージョン）

## イシュー

<u>前提条件</u>:

Cloud ライセンスは連絡先Aに関連付けられています（電子メールアドレス：*<u>first@e.mail</u>*）

<u>複製する手順</u>:

1. 連絡先Aがアカウントで作成したAdobe Commerce アクセスキー（キーX）をクラウドにインストールします。
1. 連絡先B （電子メールアドレス：*<u>second@e.mail</u>*）は、自分のアカウントを使用して拡張機能を購入し、拡張機能をインストールするためのアクセスキー（キーY）を作成しました。
1. 連絡先Aはその後会社を離れ、ライセンス（所有権）は連絡先Bに転送されました。
1. システムインテグレーターは、キーXを使用してクラウド環境に拡張機能をインストールしようとします。

<u>期待される結果</u>:

拡張機能が正常にインストールされました。

<u>実際の結果</u>:

デプロイメントが失敗したため、拡張機能はインストールされません。

## 原因

両方のキーが連絡先の役割に割り当てられるため、競合が発生します。

## Solution

（元のアカウントと新しいアカウントの両方に独自のアクセスキーが割り当てられている）アカウントのプライマリ担当者に変更が加えられ、キーが元のアカウントから新しいアカウントに転送された後にデプロイメントが失敗した場合は、元のアカウントからキーを無効にする必要があります。 上記の例では、キーXを無効にする必要があります。

### アクセスキーの無効化

古いキーに関連付けられている[Commerce Marketplace](https://marketplace.magento.com/) アカウントにアクセスできない場合は、[Adobe Commerce サポート ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)に連絡してキーを無効にしてもらってください。

古いキーに関連付けられているMarketplace アカウントにアクセスできる場合は、次の手順を実行してキーを無効にします。

1. 古いアカウントの資格情報を使用して[Commerce Marketplace](https://marketplace.magento.com/)にログインします。
1. ページの右上にあるアカウント名をクリックし、**マイプロファイル**&#x200B;を選択します。
1. 「Marketplace」タブの「**アクセスキー**」をクリックします。

   ![magento_products_access_keys_2.4.1.png](/help/troubleshooting/miscellaneous/assets/magento_products_access_keys_2.4.1.png)

1. アクセスキーの横にある「**無効化**」をクリックします。

## 関連トピックス

* [認証キーを入手](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)する方法については、開発者用ドキュメントをご覧ください。
