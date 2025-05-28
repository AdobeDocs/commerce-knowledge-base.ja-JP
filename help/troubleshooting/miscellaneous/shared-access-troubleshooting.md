---
title: 共有アクセスのトラブルシューティング
description: '**問題：**信頼できる仕事仲間への共有アクセスを提供したいが、Commerce アカウント ページで**共有アクセス** タブが見つからない。'
exl-id: 9e03c031-2359-42a6-9de4-943451a16456
feature: Cache
role: Developer
source-git-commit: c2ccad480c89b974ffea7f2d4e2860e01882f833
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# 共有アクセスのトラブルシューティング

## Commerce アカウントページ（アカウントオーナー）に「[!UICONTROL Shared Access]」タブが表示されません

**問題：** 信頼できる仕事仲間への共有アクセスを提供したいが、Commerce アカウント ページで [**[!UICONTROL Shared Access]**] タブが見つからない。

**原因：** 共有アクセスを許可するために必要なアクセス許可がCommerce アカウントに関連付けられていません。

**解決策：**

* アカウントオーナー（プライマリアカウントの所有者）の場合は、Adobe アカウントチームにお問い合わせください。 チームメンバーがサポートへのアクセス権を持っている場合は、[ サポートチケットを作成 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#merchant-not-displayed) してもらいます。 アカウントに関連付けられた名前とメールを指定します。
* アカウントの所有者でない場合は、所有者に連絡して共有アクセスおよび必要な権限を提供してもらう必要があります。
* アカウント所有者が会社を終了し、アカウントを別のユーザーに転送する場合は、[Commerce アカウントの転送 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-transfer) を参照してください。

>[!NOTE]
>
>アカウント所有者以外のユーザーでも、自分のアカウントに「[!UICONTROL Shared Access]」タブを設定することは可能です。 ただし、他のユーザーに共有アクセスを提供できるのは、必要な権限を持つアカウント所有者（プライマリアカウント所有者）のみです。 共有アクセスについて詳しくは、『Adobe Commerce Experience League サポートユーザーガイド』の [ 共有アクセス：自分のアカウントにアクセスするための他のユーザーへの権限の付与 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#shared-access) を参照してください。

## 共有アクセスを使用しましたが、特定のリソースにアクセスできません

**問題：** [!UICONTROL Shared Access] アカウントに切り替えましたが、**[!UICONTROL Support tab]** にアクセスできません（例：）。

**考えられる原因：** サポートの使用権限が期限切れになったか、サポートへの共有アクセスが許可されていません。

**解決策：**

1. **[!UICONTROL My Account]** に戻ります。
1. 「**[!UICONTROL Shared with me]**」タブをクリックします。
1. 問題が発生している **[!UICONTROL Shared Access]** アカウントをクリックし、アクセス権が付与されているリソースを確認します。
1. 特定のリソースがない場合は、アカウント所有者（プライマリアカウント所有者）にお問い合わせください。

問題が引き続き発生する場合は、Adobe アカウントチームにお問い合わせください。 アカウントに関連付けられた名前とメールを指定します。

## 共有アクセスを使用して [!UICONTROL Support] をクリックしましたが、組織の新しいチケットを開いたとき、フォームで使用できる製品がありませんでした

**問題：**[Experience Leagueでチケットを開く際に、適切なクラウドプロジェクトを選択できない ](https://experienceleague.adobe.com/home#support)。

**考えられる原因：** 資格が [!DNL Commerce] い正しい組織が選択されていません。

**解決策：**

1. （[!DNL Commerce]）サフィックスの付いた組織を選択してください。 これは、[!DNL Commerce] の使用権限を持つ組織です。

問題が引き続き発生する場合は、Adobe アカウントチームにお問い合わせください。 アカウントに関連付けられた名前とメールを指定します。

## 共有アクセスを使用して [!UICONTROL Support] をクリックしましたが、[!DNL Commerce] の使用権限を持つ組織の新しいチケットを開くと、クラウドプロジェクトがフォームにリストされませんでした

**問題**:[Experience League](https://experienceleague.adobe.com/home#support) でチケットを開く際に、適切なクラウドプロジェクトを選択できません。

**考えられる原因**: プロジェクトに追加されていない、またはプロジェクトが別のライセンスに関連付けられている可能性があります（一部の組織は、非常に似た名前を持つ子会社/関連会社を持っています）。

**解決策**:

1. プロジェクトに追加されていることを確認します。 [ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access) を参照してください。
1. プロジェクトに関連付けられたライセンスに対する共有アクセスが、アカウント所有者から付与されていることを確認します。

問題が引き続き発生する場合は、Adobe アカウントチームにお問い合わせください。 アカウントに関連付けられた名前とメールを指定します。

## 共有アクセスを使用して [!UICONTROL Support] をクリックしましたが、新しいチケットを開いたときに、[!UICONTROL Organization] のドロップダウンが表示されなかったか、その組織がリストされていませんでした

**問題**: [!UICONTROL Shared Access] アカウントに切り替えましたが、[Experience League](https://experienceleague.adobe.com/home#support) でチケットを送信しようとすると、組織が使用できないか、組織名がドロップダウンに表示されません。

**考えられる原因**: アカウント内の 1 つのマーチャントに対してのみ共有アクセスが許可されています。

**解決策**:

1. **[!UICONTROL My Account]** に戻ります。
1. 1 つの共有名のみがリストされている場合、その共有名がチケットを開くデフォルトの組織になります。

問題が引き続き発生する場合は、Adobe アカウントチームにお問い合わせください。 アカウントに関連付けられた名前とメールを指定します。

## 共有アクセスを使用しましたが、共有アクセスではなくチケットが表示されます

**問題：** 共有アクセスを使用して [ ヘルプセンター ](https://support.magento.com/hc/us-en/requests) にアクセスしていますが、自分のアカウント（組織）に属するチケットのみが表示されます。 [!DNL Commerce] アカウント ページに、共有アクセスを提供してくれた組織のアカウントを使用していることが表示されますが、組織のチケットはまだ表示されていません。

**考えられる原因：** ブラウザーがヘルプ センターからキャッシュされたコンテンツを使用しています。

**解決策：** ブラウザーのキャッシュをクリアして、ヘルプセンターに再度アクセスします（Commerce アカウントのページで共有アクセスに切り替えていることを確認します）。

## 関連資料

* [Adobe Commerce サポートまたは Cloud アカウントにログインできない ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/unable-to-log-in-to-support-or-cloud-project)
* [MageID アカウント所有者がログインしてサポートチケットを送信できません ](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25231)
