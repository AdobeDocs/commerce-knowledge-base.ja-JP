---
title: Magento.comとaccounts.magento.cloud アカウントのログイン情報をリンク
description: 2020年4月1日現在、Adobe Commerceでは、[accounts.magento.cloud] （https://accounts.magento.cloud/）にアカウントを持つユーザーは、このアカウントを[Magento.com] （https://account.magento.com/customer/account/login/）アカウントにリンクする必要があります。 これにより、[Magento.com] （https://account.magento.com/customer/account/login/） アカウントのログインが両方のアカウントのプライマリログイン方法になり、ユーザーのセキュリティが向上します。
exl-id: 89afec50-bc21-46cd-8440-2bcf717ded69
feature: Cloud
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%
---
# Magento.comとaccounts.magento.cloud アカウントのログイン情報をリンク

2020年4月1日現在、Adobe Commerceでは、[accounts.magento.cloud](https://accounts.magento.cloud/)のアカウントを持つユーザーは、このアカウントを[Magento.com](https://account.magento.com/customer/account/login/) アカウントとリンクする必要があります。 これにより、[Magento.com](https://account.magento.com/customer/account/login/) アカウントのログインが両方のアカウントのプライマリログイン方法になり、ユーザーのセキュリティが向上します。

[accounts.magento.cloud](https://accounts.magento.cloud/)のユーザーは、次の2つの方法のいずれかで、これらのアカウントを接続できます。

## 方法1

1. お好みの方法でログインした後、[https://accounts.magento.cloud/user](https://accounts.magento.cloud/user)の&#x200B;**アカウント設定**&#x200B;に移動します。
1. ページの&#x200B;**シングルサインオン** セクションを開きます。
1. **Provider: Magento.com**&#x200B;が「ステータスが接続されていません」と報告した場合は、**Magento.comとの接続** ボタンを選択します。
1. [https://account.magento.com/applications/customer/login/](https://account.magento.com/applications/customer/login/)にリダイレクトされます。
1. そこから、Adobe Commerce アカウントを作成するか、既存のアカウントにログインできます。

## 方法2

1. [https://account.magento.com](https://account.magento.com/)にログインします。
1. 別のタブに移動して、[https://accounts.magento.cloud/user](https://accounts.magento.cloud/user)に移動します。
1. 「[Magento.com](https://account.magento.com/customer/account/login/)」をクリックします。

## 関連トピックス

* [Adobe Commerce サポートまたはクラウドアカウントにログインできない](/help/troubleshooting/miscellaneous/unable-to-log-in-to-support-or-cloud-project.md)
* [MageID アカウント所有者がログインしてサポートチケットを送信できない](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25231)
