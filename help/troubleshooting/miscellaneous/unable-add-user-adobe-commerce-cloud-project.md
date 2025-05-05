---
title: Adobe Commerce クラウドプロジェクトにユーザーを追加できない
description: ここでは、Adobe Commerce クラウドプロジェクトにユーザーを追加できない場合の解決策を説明します。
exl-id: 59940916-bf92-4e89-a6f9-bca87c54125c
feature: Cloud, Paas
role: Developer
source-git-commit: af74d944553c34da2ac8343695bca49f971bc4e5
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Adobe Commerce クラウドプロジェクトにユーザーを追加できない

この記事では、クラウドプロジェクトにユーザーを追加しようとして、*ユーザー XXX が存在しません* というエラーが発生して追加できない場合の解決策を説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## 問題

ここでは、Adobe Commerce クラウドプロジェクトにユーザーを追加できない場合の解決策を説明します。

## 原因：

これは想定されている動作です。 ユーザーのアカウントは、まずhttps://accounts.magento.cloudで作成し、Adobe SSO にリンクして、ユーザーとしてプロジェクトに追加されるようにする必要があります。

## 解決策

1. https://accounts.magento.cloudで自分のアカウントにログインするようにユーザーに依頼します（ユーザーは、そのメールアドレスでadobe.comのアカウントに既に登録している必要があります）。 https://account.adobe.comでアカウントを作成または持っていることは、ユーザーがhttps://accounts.magento.cloudでアカウントを持つことを自動的に意味するものではありません）
メモ：2022 年 8 月より前に、ユーザーがaccount.magento.comまたは accounts.magento.cloud にアカウントを持っている場合、2022 年 8 月以降に作成した場合を除き、ユーザーがadobe.comにアカウントを持っていない可能性があります。 ユーザーがAdobeアカウントを持っていて、ログインできない場合は、https://experienceleague.adobe.com/home?lang=ja#supportで [ サポートリクエストを送信 ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) し、詳細を入力してください（問題の理由= User Management）。
1. 次に、https://accounts.magento.cloudに移動します。
1. 完了したら、ユーザーをプロジェクトに追加できます。 手順については、Cloud Infrastructure のCommerce ガイドの [ ユーザーの追加とアクセスの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#add-users-and-manage-access) を参照してください。

## 関連資料：

* Commerce on Cloud Infrastructure ガイドの [ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja)。
* [Adobe Commerce サポートまたは Cloud アカウントにログインできない ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/unable-to-log-in-to-support-or-cloud-project.html?lang=ja)
