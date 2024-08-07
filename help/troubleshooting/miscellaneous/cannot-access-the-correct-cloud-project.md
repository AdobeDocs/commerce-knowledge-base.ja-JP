---
title: 正しいAdobe Commerce アカウント / プロジェクトにアクセスできないか、プロジェクトがアカウントにありません
description: ここでは、所有権やメールアドレスに変更がある場合に、正しい cloud Adobe Commerce プロジェクトにアクセスできない場合の問題を修正します。
exl-id: 165b9a18-6e84-4f0f-b377-a07152d55c9e
hide: true
hidefromtoc: true
feature: Cloud, Paas
role: Developer
source-git-commit: 423a392eb32df69c38b84081ac2ed17ae1efdc7b
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# 正しいクラウドアカウント / プロジェクトにアクセスできないか、プロジェクトがアカウントにありません

この記事では、アカウントの所有権または関連するメールアドレスに変更が加えられた後の次の問題を修正します。

1. 正しい Cloud Adobe Commerce プロジェクトにアクセスできません。
1. [accounts.magento.cloud/user](https://accounts.magento.cloud/user) のアカウントの下にクラウドAdobe Commerce プロジェクトが表示されません。
1. 別のアカウント（例：以前のアカウント所有者）の詳細が [accounts.magento.cloud/user](https://accounts.magento.cloud/user) に表示されています。

## 問題

所有権やメールアドレスに変更がある場合、正しい Cloud Adobe Commerce プロジェクトにアクセスできません。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 原因：

この問題は、通常、次の期間が経過した後も、以前のプロジェクト所有者のシングルサインオン（SSO）が引き続きAdobe.comと統合されている場合に発生します。

1. クラウドプロジェクトの所有権が（ユーザーの）自分に転送され、元のプロジェクト所有者のアカウントが表示されています。 [ ソリューション ](#solution-for-cause-one-and-two) についてはここをクリックしてください。

   または

1. ユーザーが別の会社に移動し、メールアドレスとアクセス権のあるプロジェクトが変更された。 以前の役割/会社でアクセス権を付与されていたプロジェクトが表示されます。 [ ソリューション ](#solution-for-cause-one-and-two) についてはここをクリックしてください。

   または

1. https://account.adobe.comのメールアドレスを、現在クラウドプロジェクトに関連付けられていない別のメールアドレスに変更しました。 [ ソリューション ](#solution-for-cause-three) についてはここをクリックしてください。

## 原因 1 と 2 の解決策 {#solution-for-cause-one-and-two}

この問題の原因が 1 と 2 である場合の解決策は、Adobe.comとのシングルサインオン統合を切断することです。 接続解除するには、次の手順に従います。

1. https://accounts.magento.cloud/userから、「**[!UICONTROL Single Sign-On]**」セクションを展開します。 **[!UICONTROL Disconnect from Adobe.com]** をクリックして接続を解除します。

   ![adobe-connect のシングルサインオン ](assets/sso-adobe-disconnect.png)

1. 「**[!UICONTROL Disconnect]**」をクリックします。

   ![adobe-disconnect](assets/adobe-disconnect.png)

1. ログアウトします。
1. 「**[!UICONTROL Adobe.com]**」ボタンをクリックします。

   ![Magento.com](assets/adobe-welcome-login.png)

1. これで、正しいアカウントが表示され、正しいクラウドプロジェクトにアクセスできるようになります。

## 原因 3 の解決策 {#solution-for-cause-three}

問題が原因で発生している場合は、プロジェクトの既存のスーパーユーザーに、新しいメールアドレスをプロジェクトに追加するように依頼します。 詳しくは、[ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html) を参照してください。
