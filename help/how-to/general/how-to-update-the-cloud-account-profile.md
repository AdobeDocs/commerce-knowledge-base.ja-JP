---
title: クラウドアカウントプロファイルの更新方法
description: この記事では、クラウドアカウントのプロファイルを変更する手順を説明します。
feature: Cloud, Support
role: Admin, Developer
exl-id: b0c9dbcf-9745-494d-a662-80c5c6378068
source-git-commit: bc8dbb1b43c3f2ad8f2ac214fd303f6a4d3e3412
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# クラウドアカウントプロファイルの更新方法

この記事では、クラウドアカウントのプロファイルを変更する手順を説明します。

## Solution

クラウドアカウントのプロファイルを変更する場合、次のフィールドを変更できます。

1. [!UICONTROL First name]
1. [!UICONTROL Last name]
1. [!UICONTROL Username]

   >[!NOTE]
   >
   >Cloud Console ユーザー名を更新すると、プロジェクト URLが`https://console.adobecommerce.com <old-username>/<project-id>`から`https://console.adobecommerce.com/<new-username>/<project-id>`に変更されます。
   >
   >更新後、古いURLを使用するリンクは機能しなくなります。 チームメンバーは、新しいURLを使用するために、保存されたブックマーク、内部ドキュメント、および自動化を更新する必要があります。
   >
   >この変更は、新しいCloud Console URLにのみ適用されます。 レガシープロジェクト URL （`https://<region>.magento.cloud/projects/<project-id>`）はユーザー名を使用せず、変更なしで引き続き機能します。

これらのフィールドを変更するには、次の手順に従います。

1. [Adobe アカウントのログイン &#x200B;](https://accounts.magento.cloud)でアカウントにアクセスします。
1. 「**[!UICONTROL Account Settings]**」タブをクリックします。
1. 「*新しいパスワードを作成*」チェックボックスを選択します。
1. 必要な変更を行い、*保存*&#x200B;をクリックします。

>[!NOTE]
>
>パスワードは変更されません。

## 変更できないものは何か？

1. **[!UICONTROL Password]**:
パスワードを変更するには、[Adobe password reset](https://account.adobe.com/)にアクセスしてください。このプロファイルは、アカウントまたはメールアドレスにリンクされています。

1. **[!UICONTROL Email Address]**:
このフィールドの変更は、個々の状況によって異なります。

現在のアカウントの所有権を新しい所有者または別のメールアドレスに転送する必要がある場合は、アカウントに関連付けられているプライマリユーザーメールを更新する必要があります。

参照：[https://experienceleague.adobe.com/docs/commerce-admin/start/commerce-account/commerce-account-transfer.html?lang=ja](https://experienceleague.adobe.com/docs/commerce-admin/start/commerce-account/commerce-account-transfer.html?lang=ja)
