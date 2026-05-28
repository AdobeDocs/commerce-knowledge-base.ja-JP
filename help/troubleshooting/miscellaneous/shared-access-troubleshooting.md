---
title: 共有アクセスのトラブルシューティング
description: '** 問題：**信頼できる同僚に共有アクセスを提供する必要がありますが、Commerce アカウントページの「**Shared Access**」タブを見つけることができません。'
exl-id: 9e03c031-2359-42a6-9de4-943451a16456
feature: Cache
role: Developer
source-git-commit: c9ad6040ddb65dbb3be6591f2c0e00405dfbebd5
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# 共有アクセスのトラブルシューティング

## Commerce アカウントページに「[!UICONTROL Shared Access]」タブが表示されない（アカウントオーナー）

**問題：**&#x200B;信頼できる同僚に共有アクセスを提供する必要がありますが、Commerce アカウント ページで「**[!UICONTROL Shared Access]**」タブが見つかりません。

**考えられる原因：**&#x200B;共有アクセス権の付与に必要な権限が、Commerce アカウントに関連付けられていません。

**解決策：**

* アカウント所有者（プライマリアカウント所有者）の場合は、Adobe アカウントチームにお問い合わせください。 チームメンバーがサポートにアクセスできる場合は、[ サポートチケットを作成してもらいます](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#merchant-not-displayed)。 アカウントに関連付けられている名前とメールアドレスを指定します。
* アカウント所有者でない場合は、共有アクセスと必要な権限を提供するために、アカウント所有者に連絡する必要があります。
* アカウント所有者が会社に所属していない場合に、アカウントを別のユーザーに転送する場合は、[Commerce アカウントの転送](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-transfer)を参照してください。

>[!NOTE]
>
>アカウント以外の所有者でも、アカウントに「[!UICONTROL Shared Access]」タブを持つことができます。 ただし、必要な権限を持つアカウント所有者（プライマリアカウント所有者）のみが、他のユーザーに共有アクセスを提供できます。 共有アクセスについて詳しくは、Adobe CommerceのExperience League サポートユーザーガイドの「[共有アクセス：他のユーザーがアカウントにアクセスするための権限を付与する](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#shared-access)」を参照してください。

## 共有アクセスを使用しましたが、特定のリソースにアクセスできません

**問題：** [!UICONTROL Shared Access] アカウントに切り替えましたが、**[!UICONTROL Support tab]**&#x200B;にアクセスできません（例）。

**考えられる原因：** サポートの使用権限が期限切れになっているか、サポートへの共有アクセスが許可されていません。

**解決策：**

1. **[!UICONTROL My Account]**&#x200B;に切り替えます。
1. 「**[!UICONTROL Shared with me]**」タブをクリックします。
1. 問題がある&#x200B;**[!UICONTROL Shared Access]** アカウントをクリックし、アクセス権が付与されているリソースを確認します。
1. 特定のリソースが見つからない場合は、アカウントオーナー（プライマリアカウント所有者）にお問い合わせください。

引き続き問題が発生する場合は、Adobeのアカウントチームにお問い合わせください。 アカウントに関連付けられている名前とメールアドレスを指定します。

## 共有アクセスを使用して[!UICONTROL Support]をクリックしましたが、組織の新しいチケットを開いたときに、フォームに利用できる製品がありませんでした

**問題：** [Experience League](https://experienceleague.adobe.com/home#support)でチケットを開く際に、適切なCloud Projectを選択できません。

**考えられる原因：** [!DNL Commerce]の使用権限を持つ正しい組織が選択されていません。

**解決策：**

1. （[!DNL Commerce]）接尾辞が付いた組織を選択してください。 これは、[!DNL Commerce]の使用権限を持つ組織です。

引き続き問題が発生する場合は、Adobeのアカウントチームにお問い合わせください。 アカウントに関連付けられている名前とメールアドレスを指定します。

## 共有アクセスを使用して[!UICONTROL Support]をクリックしましたが、[!DNL Commerce]の使用権限を持つ組織の新しいチケットを開いたときに、クラウドプロジェクトがフォームに表示されませんでした

**問題**: [Experience League](https://experienceleague.adobe.com/home#support)でチケットを開く際に、適切なCloud Projectを選択できません。

**考えられる原因**：プロジェクトに追加されていない可能性があります。または、プロジェクトが別のライセンスに関連付けられている可能性があります（一部の組織では、非常に類似した名前の子会社や関連会社がある場合があります）。

**解決策**:

1. プロジェクトに追加されていることを確認します。 [ ユーザーアクセスの管理](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access)を参照してください。
1. アカウント所有者から、プロジェクトに関連付けられたライセンスへの共有アクセス権が付与されていることを確認します。

引き続き問題が発生する場合は、Adobeのアカウントチームにお問い合わせください。 アカウントに関連付けられている名前とメールアドレスを指定します。

## 共有アクセスを使用して[!UICONTROL Support]をクリックしましたが、新しいチケットを開いたときに、[!UICONTROL Organization] ドロップダウンが表示されなかったか、その組織を一覧表示しませんでした

**問題**: [!UICONTROL Shared Access] アカウントに切り替えましたが、[Experience League](https://experienceleague.adobe.com/home#support)でチケットを送信しようとすると、利用できる組織がないか、または組織名がドロップダウンに表示されません。

**考えられる原因**：アカウント内の1人の販売者に対してのみ共有アクセスが許可されています。

**解決策**:

1. **[!UICONTROL My Account]**&#x200B;に切り替えます。
1. 1つの共有名のみをリストする場合は、チケットを開くデフォルトの組織になります。

引き続き問題が発生する場合は、Adobeのアカウントチームにお問い合わせください。 アカウントに関連付けられている名前とメールアドレスを指定します。

## 共有アクセスを使用しましたが、共有アクセスの代わりにチケットが表示されます

**問題：**&#x200B;共有アクセスを使用して[ ヘルプセンター](https://support.magento.com/hc/us-en/requests)にアクセスしていますが、自分のアカウント（組織）に属するチケットのみが表示されます。 「[!DNL Commerce] アカウント」ページには、組織のアカウントを使用していることが表示されます。このアカウントは共有アクセスを提供しましたが、組織のチケットはまだ表示されていません。

**考えられる原因：**&#x200B;お使いのブラウザーは、ヘルプセンターからキャッシュされたコンテンツを使用しています。

**解決策：** ブラウザーのキャッシュをクリアし、ヘルプセンターに再度アクセスします（Commerce アカウント ページで共有アクセスに切り替えたことを確認してください）。

## 関連トピックス

* [Adobe Commerce サポートまたはクラウドアカウントにログインできない](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/unable-to-log-in-to-support-or-cloud-project)
* [MageID アカウント所有者がログインしてサポートチケットを送信できない](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25231)
* [Commerce アカウントの共有](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-share)
