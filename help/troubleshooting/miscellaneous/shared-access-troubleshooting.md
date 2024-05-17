---
title: 共有アクセスのトラブルシューティング
description: 「**問題：**信頼できる同僚への共有アクセスを提供したいが、Commerce アカウント**ページに「共有アクセス**」タブが見つからない。」
exl-id: 9e03c031-2359-42a6-9de4-943451a16456
feature: Cache
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 共有アクセスのトラブルシューティング

## が表示されません。 [!UICONTROL Shared Access] Commerce アカウントページ（アカウントオーナー）の Tab

**問題：** 信頼できる仕事仲間に共有アクセスを提供したいが、が見つからない **[!UICONTROL Shared Access]** Commerce アカウントページでタブを選択します。

**考えられる原因：** 共有アクセスを許可するために必要な権限がCommerce アカウントに関連付けられていません。

**解決策：** アカウントオーナー（プライマリアカウント所有者）の場合は、Adobeアカウントチームにお問い合わせください。または [サポートチケットを作成](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed). 名前とアカウントに関連付けられたメールアドレスを指定してください。

>[!NOTE]
>
>アカウント所有者でなくても、次の権限を持つことができます **[!UICONTROL Shared Access]** ユーザーのアカウントで Tab キーを押します。 ただし、他のユーザーに共有アクセスを許可できるのは、適切な権限を持つアカウント所有者（プライマリアカウント所有者）のみです。 共有アクセスの詳細については、を参照してください。 [共有アクセス：自分のアカウントにアクセスするための権限を他のユーザーに付与します](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#shared-access) （Adobe Commerce ヘルプセンターユーザーガイド）。

## 共有アクセスを使用しましたが、特定のリソースにアクセスできません

**問題：** 共有アクセスアカウントに切り替えましたが、にアクセスできません **[!UICONTROL Support tab]** （例えば）。

**考えられる原因：** サポートの使用権限が期限切れになったか、サポートへの共有アクセスが許可されていません。

**解決策：**

1. 切り替え先 **[!UICONTROL My Account]**.
1. 次に、 **[!UICONTROL Shared with me]** タブ。
1. 「」をクリック **[!UICONTROL Shared Access]** 問題が発生しているアカウントで、アクセス権が付与されているリソースを調べます。
1. 指定したリソースがない場合は、アカウントオーナー（プライマリアカウント所有者）にお問い合わせください。

引き続き問題が発生する場合は、Adobeアカウントチームに問い合わせるか、grp-Magento-HelpCenterLoginIssues@adobe.comまでメールを送信してください。 名前とアカウントに関連付けられたメールアドレスを指定してください。

## 共有アクセスを使用してクリックしました [!UICONTROL Support]しかし、新しいチケットを開くと、 [!UICONTROL Organization] ドロップダウンが表示されない

**問題：** 共有アクセスアカウントに切り替えましたが、にアクセスできません **[!UICONTROL Support tab]** （例えば）。

**考えられる原因：** アカウント内の 1 つのマーチャントに対してのみ共有アクセスが許可されています。

**解決策：**

1. 切り替え先 **[!UICONTROL My Account]**.
1. 1 つのみ表示される場合 **[!UICONTROL Shared Name]**。これは *デフォルトの組織* チケットが下に開かれること。

引き続き問題が発生する場合は、Adobeアカウントチームに問い合わせるか、grp-Magento-HelpCenterLoginIssues@adobe.comまでメールを送信してください。 名前とアカウントに関連付けられたメールを指定します。

## 共有アクセスを使用しましたが、共有アクセスではなくチケットが表示されます

**問題：** 共有アクセスを使用してヘルプセンターにアクセスしていますが、自分のアカウント（組織）に属するチケットのみが表示されます。 「Commerceアカウント」ページに、共有アクセスを提供してくれた組織のアカウントを使用していることが表示されますが、組織のチケットはまだ表示されていません。

**考えられる原因：** ブラウザーは、ヘルプセンターからキャッシュされたコンテンツを使用しています。

**解決策：** ブラウザーのキャッシュをクリアして、ヘルプセンターに再度アクセスします（Commerce アカウントのページで共有アクセスに切り替えていることを確認します）。

## 関連資料

[チケット送信フォーム：組織ドロップダウンにマーチャントが表示されない](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed) サポートナレッジベースで。
