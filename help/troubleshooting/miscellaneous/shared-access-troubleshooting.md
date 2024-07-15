---
title: 共有アクセスのトラブルシューティング
description: 「**問題：**信頼できる同僚への共有アクセスを提供したいが、Commerce アカウント**ページに「共有アクセス**」タブが見つからない。」
exl-id: 9e03c031-2359-42a6-9de4-943451a16456
feature: Cache
role: Developer
source-git-commit: e77322c04c7245538c10dfb397094eee6cfe6be9
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 共有アクセスのトラブルシューティング

## Commerce アカウントページ（アカウントオーナー）に「[!UICONTROL Shared Access]」タブが表示されません

**問題：** 信頼できる仕事仲間への共有アクセスを提供したいが、Commerce アカウント ページで [**[!UICONTROL Shared Access]**] タブが見つからない。

**原因：** 共有アクセスを許可するために必要なアクセス許可がCommerce アカウントに関連付けられていません。

**解決策：** アカウントオーナー（プライマリアカウントホルダー）の場合は、Adobeアカウントチームに問い合わせるか、[ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed) してください。 名前とアカウントに関連付けられたメールアドレスを指定してください。

>[!NOTE]
>
>アカウント所有者以外のユーザーでも、自分のアカウントに「**[!UICONTROL Shared Access]**」タブを設定することは可能です。 ただし、他のユーザーに共有アクセスを許可できるのは、適切な権限を持つアカウント所有者（プライマリアカウント所有者）のみです。 共有アクセスの詳細については、Adobe Commerce ヘルプセンターユーザーガイドの [ 共有アクセス：自分のアカウントに他のユーザーがアクセスするための権限の付与 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#shared-access) を参照してください。

## 共有アクセスを使用しましたが、特定のリソースにアクセスできません

**問題：** 共有アクセスアカウントに切り替えましたが、**[!UICONTROL Support tab]** にアクセスできません（例：）。

**考えられる原因：** サポートの使用権限が期限切れになっているか、サポートへの共有アクセスが許可されていません。

**解決策：**

1. **[!UICONTROL My Account]** に戻ります。
1. 次に、「**[!UICONTROL Shared with me]**」タブをクリックします。
1. 問題が発生している **[!UICONTROL Shared Access]** アカウントをクリックし、アクセス権が付与されているリソースを確認します。
1. 指定したリソースがない場合は、アカウントオーナー（プライマリアカウント所有者）にお問い合わせください。

引き続き問題が発生する場合は、Adobeアカウントチームに問い合わせるか、grp-Magento-HelpCenterLoginIssues@adobe.comまでメールを送信してください。 名前とアカウントに関連付けられたメールアドレスを指定してください。

## 共有アクセスを使用して [!UICONTROL Support] をクリックしましたが、新しいチケットを開くと、[!UICONTROL Organization] ドロップダウンが表示されません

**問題：** 共有アクセスアカウントに切り替えましたが、**[!UICONTROL Support tab]** にアクセスできません（例：）。

**考えられる原因：** アカウントの 1 つのマーチャントに対する共有アクセスのみが許可されています。

**解決策：**

1. **[!UICONTROL My Account]** に戻ります。
1. リストに **[!UICONTROL Shared Name]** が 1 つだけの場合、チケットが開かれる *デフォルトの組織* になります。

引き続き問題が発生する場合は、Adobeアカウントチームに問い合わせるか、grp-Magento-HelpCenterLoginIssues@adobe.comまでメールを送信してください。 名前とアカウントに関連付けられたメールを指定します。

## 共有アクセスを使用しましたが、共有アクセスではなくチケットが表示されます

**問題：** 共有アクセスを使用してヘルプセンターにアクセスしていますが、自分のアカウント（組織）に属するチケットのみが表示されます。 「Commerceアカウント」ページに、共有アクセスを提供してくれた組織のアカウントを使用していることが表示されますが、組織のチケットはまだ表示されていません。

**考えられる原因：** ブラウザーがヘルプ センターからキャッシュされたコンテンツを使用しています。

**解決策：** ブラウザーのキャッシュをクリアして、ヘルプセンターに再度アクセスします（Commerce アカウントのページで共有アクセスに切り替えていることを確認します）。

## 関連資料

[ チケット送信フォーム：マーチャントが、サポートナレッジベースの「組織」ドロップダウンに表示されません ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#merchant-not-displayed)。
