---
title: クラウドインフラストラクチャ UI 上のAdobe Commerceにアクセスできない
description: この記事では、クラウドインフラストラクチャ UI 上のAdobe Commerceにログインすると「403 エラー」が発生する問題の解決策を説明します。
exl-id: 948e4acd-abd6-4562-b9c0-771a977188ba
feature: Cloud, Paas
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# クラウドインフラストラクチャ UI 上のAdobe Commerceにアクセスできない

この記事では、クラウドインフラストラクチャ UI 上のAdobe Commerceにログインすると *403 エラー* が発生する問題の解決策を説明します。

## 問題

クラウドインフラストラクチャ UI 上でAdobe Commerceに初めてログインしようとすると、「*403:Environment Access Denied*」エラーが発生する。 このエラーは、クラウド URL に初めて移動するとマスターブランチが読み込まれ、そのブランチにアクセスできない可能性があるために発生する場合があります。

## 解決策

URL に初めてアクセスするときに 403 エラーが発生した場合は、マスターブランチに役割があることを確認します。

1. сプロジェクトでライセンス所有者またはスーパーユーザーに連絡し、開発者ドキュメントの **クラウドプロジェクト/Cloud Console からのユーザーの管理** にも記載されている [&#x200B; 環境レベルのユーザー &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#manage-users-from-the-cloud-console) としてアクセス権を提供していることを確認します。

   特定のブランチで適用可能な役割のみが存在する場合は、そのブランチの URL に移動する必要があります（例：）。
   `https://console.adobecommerce.com/<owner-name>/<project-id>/<branch-name>`

   次回メイン URL にアクセスするときは、最後にアクセスした環境がデフォルトで使用されます。

1. それでもログインできない場合はсプロジェクトにライセンス所有者またはスーパーユーザーに連絡し、開発者ドキュメントの **クラウドプロジェクト/プロジェクトにユーザーを追加** で説明されているように、[&#x200B; プロジェクトレベルのユーザー &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#add-a-user-to-the-project) としてアクセス権が提供されていることを確認してください。
1. エラーが解決しない場合は、[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) します。
