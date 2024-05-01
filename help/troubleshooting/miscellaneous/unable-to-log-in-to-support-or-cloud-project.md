---
title: Adobe Commerce サポートまたは Cloud アカウントにログインできない
description: この記事では、Adobe Commerce サポートやクラウドプロジェクトへのログインに苦労する場合のソリューションを提供します。
exl-id: 676b32d2-8197-4c60-a1b1-3c51b01dd3a3
feature: Cloud, Paas
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Adobe Commerce サポートまたは Cloud アカウントにログインできない

この記事では、Adobe Commerce サポートやクラウドプロジェクトへのログインに苦労する場合のソリューションを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法）すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 問題

に移動すると、 [https://account.magento.com/customer/account/login/](https://account.magento.com/customer/account/login/) または [https://accounts.magento.cloud/user](https://accounts.magento.cloud/user) 統合ログインフォームが表示され、以前と同じように資格情報を入力できなくなることに気付くかもしれません。

<u>再現手順</u>:

Commerce アカウントにログインしてみてください。

![adobe-login-one](assets/adobe-login-one.png)

<u>期待される結果</u>:

正常にログインしました。

<u>実際の結果</u>:

ページにリダイレクトされてAdobeアカウントでログインすると、資格情報が機能しない。

![adobe-login-two](assets/adobe-login-two.png)


## 原因：

Adobe Commerceを他のAdobeソリューションと統合するプロセスの一環として、すべてのユーザーは、MageID に接続された同じメールアドレスを使用して（まだ持っていない場合は）Adobeログインを作成する必要があります。

## 解決策

以下を使用してアカウントにログインします。

- 既存のAdobeの会社/個人アカウント。
- Adobeアカウントがない場合は、同じメールアドレスで作成します。

手順については、を参照してください。 [Commerce Identity Manager](https://experienceleague.adobe.com/docs/commerce-admin/start/commerce-account/commerce-identity-manager.html) Adobe Experience Leagueで。

## 関連資料

- [Magento.comと accounts.magento.cloud アカウントのログインにリンクします](/help/faq/general/linking-magento-com-and-accounts-magento-cloud-account-logins.md)
