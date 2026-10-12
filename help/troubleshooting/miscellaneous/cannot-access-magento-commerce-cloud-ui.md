---
title: クラウドインフラストラクチャ UI上のAdobe Commerceにアクセスできない
description: この記事では、Adobe Commerce on cloud infrastructure UIにログインできず、「403 エラー」が表示される問題の解決策を説明します。
exl-id: 948e4acd-abd6-4562-b9c0-771a977188ba
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
source-wordcount: '332'
ht-degree: 0%
---
# クラウドインフラストラクチャ UI上のAdobe Commerceにアクセスできない

この記事では、Adobe Commerce on cloud infrastructure UIにログインできず、*403 エラー*&#x200B;が発生する問題の解決策を説明します。

## イシュー

クラウドインフラストラクチャ上のAdobe Commerce UIに初めてログインしようとすると、「*403：環境アクセス拒否*」エラーが発生します。 このエラーは、初めてクラウド URLに移動するとマスターブランチが読み込まれ、そのブランチにアクセスできない可能性があるために発生する可能性があります。

## Solution

初めてURLにアクセスする際に403 エラーが発生した場合は、マスターブランチに役割があることを確認してください。

1. Сプロジェクトのライセンス所有者またはスーパーユーザーに連絡し、**環境レベルのユーザー**&#x200B;としてアクセスを提供していることを確認します。詳しくは、開発者ドキュメントの[ クラウドプロジェクト/クラウドコンソールからユーザーを管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html#manage-users-from-the-cloud-console)で説明しています。

   特定のブランチに該当する役割のみを持っている場合は、そのブランチのURLに移動する必要があります（例：
   `https://console.adobecommerce.com/<owner-name>/<project-id>/<branch-name>`

   次回メイン URLにアクセスすると、最後にアクセスした環境がデフォルトで使用されます。

1. それでもログインできない場合は、сプロジェクトのライセンス所有者またはスーパーユーザーに連絡し、[ クラウドプロジェクト/プロジェクトにユーザーを追加](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html#add-a-user-to-the-project)の説明に従って、**プロジェクトレベルのユーザー**&#x200B;としてアクセス権を提供していることを確認してください。
1. エラーが解決しない場合は、[ サポートチケットを送信](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)してください。
