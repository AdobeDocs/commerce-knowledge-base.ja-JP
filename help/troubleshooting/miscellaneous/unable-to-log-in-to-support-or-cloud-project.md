---
title: Adobe Commerce サポートまたはクラウドアカウントにログインできない
description: この記事では、Adobe Commerce サポートまたはクラウドプロジェクトにログインするのに苦慮している場合の解決策を提供します。
exl-id: 676b32d2-8197-4c60-a1b1-3c51b01dd3a3
feature: Cloud, Paas
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%
---
# Adobe Commerce サポートまたはクラウドアカウントにログインできない

この記事では、Adobe Commerce サポートまたはクラウドプロジェクトにログインするのに苦慮している場合の解決策を提供します。

## 影響を受ける製品とバージョン

Adobe Commerce （すべてのデプロイメント方法）すべての[&#x200B; サポートされているバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## イシュー

[https://account.magento.com/customer/account/login/](https://account.magento.com/customer/account/login/)または[https://accounts.magento.cloud/user](https://accounts.magento.cloud/user)に移動すると、統合ログインフォームが作成され、以前と同じように資格情報を入力できないことに気付く可能性があります。

<u>複製する手順</u>:

Commerce アカウントにログインしてみてください。

![adobe-login-one](assets/adobe-login-one.png)

<u>期待される結果</u>:

正常にログインしました。

<u>実際の結果</u>:

Adobe アカウントでログインするためのページにリダイレクトされ、資格情報が機能しない。

![adobe-login-two](assets/adobe-login-two.png)


## 原因

Adobe Commerceを他のAdobe ソリューションと統合するプロセスの一環として、すべてのユーザーは、MageIDに接続された同じメールアドレスを使用して、Adobe ログインを作成する必要があります（まだ作成していない場合）。

## Solution

次の方法でアカウントにログインできます。

- 既存のAdobeの法人/個人アカウント。
- Adobe アカウントをお持ちでない場合は、同じメールアドレスでアカウントを作成します。

手順については、Adobe Experience Leagueの[Commerce Identity Manager](https://experienceleague.adobe.com/docs/commerce-admin/start/commerce-account/commerce-identity-manager.html?lang=ja)を参照してください。

## 関連トピックス

- [Magento.comとaccounts.magento.cloud アカウントのログイン情報をリンク](/help/faq/general/linking-magento-com-and-accounts-magento-cloud-account-logins.md)
