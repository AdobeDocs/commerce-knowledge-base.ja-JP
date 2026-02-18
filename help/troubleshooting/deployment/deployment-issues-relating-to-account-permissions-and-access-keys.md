---
title: アカウント権限およびアクセスキーに関するデプロイメントの問題
description: この記事では、アクセスキー所有権の競合が原因で発生する、クラウドインフラストラクチャへのAdobe Commerceのデプロイに関する問題の解決策について説明します。
exl-id: e8d72ebe-453f-4d18-a25e-c76e685aa667
feature: Deploy, Roles/Permissions
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# アカウント権限およびアクセスキーに関するデプロイメントの問題

この記事では、アクセスキー所有権の競合が原因で発生する、クラウドインフラストラクチャへのAdobe Commerceのデプロイに関する問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（サポート対象のすべてのバージョン）

## 問題

<u> 前提条件 </u>:

クラウド ライセンスは連絡先 A （E メール アドレス：*<u>first@e.mail</u>*）に関連付けられています

<u> 再現手順 </u>:

1. A 担当者のアカウントに作成したAdobe Commerce アクセスキー（キー X）に連絡して、クラウドにインストールする。
1. B 担当者（メールアドレス : *<u>second@e.mail</u>*）が自分のアカウントを使用して拡張機能を購入し、拡張機能をインストールするためのアクセスキーを作成しました（キー Y）。
1. A に連絡して会社を辞め、ライセンス（所有権）は B に転送されました。
1. システムインテグレーターは、キー X を使用してクラウド環境に拡張機能をインストールしようとします。

<u> 期待される結果 </u>:

拡張機能が正常にインストールされました。

<u> 実際の結果 </u>:

展開が失敗したため、拡張機能はインストールされません。

## 原因：

両方のキーが連絡先の役割に割り当てられるので、競合が発生します。

## 解決策

アカウントのプライマリ連絡先に変更を加えた後にデプロイに失敗し（元のアカウントと新しいアカウントの両方に独自のアクセスキーがあり）、キーが元のアカウントから新しいアカウントに転送された場合は、元のアカウントのキーを無効にする必要があります。 上記の例では、キー X を無効にする必要があります。

### アクセスキーを無効にする方法

古いキーに関連付けられた [Commerce Marketplace](https://marketplace.magento.com/) アカウントにアクセスできない場合は、[Adobe Commerce サポートにお問い合わせ &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) してキーを無効にしてください。

古いキーに関連付けられた Marketplace アカウントにアクセスできる場合は、次の手順を実行してキーを無効にします。

1. 古いアカウントの資格情報を使用して [Commerce Marketplace&rbrace; にログインします。](https://marketplace.magento.com/)
1. ページの右上にあるアカウント名をクリックし、「**マイプロファイル**」を選択します。
1. 「Marketplace」タブの **アクセスキー** をクリックします。

   ![magento_products_access_keys_2.4.1.png](/help/troubleshooting/miscellaneous/assets/magento_products_access_keys_2.4.1.png)

1. アクセスキーの横にある **無効** をクリックします。

## 関連資料

* [&#x200B; 認証キーの取得 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) については、開発者向けドキュメントを参照してください。
