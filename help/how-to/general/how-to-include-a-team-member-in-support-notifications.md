---
title: サポート通知にチームメンバーを含める方法
description: この記事では、サポート通知にチームメンバーを含める方法について説明します。
feature: Cloud, Support, Admin Workspace
role: Admin, Developer
exl-id: 63ea3f60-a509-447c-ac3d-bb2133141c80
source-git-commit: 1c568d75534bbfe322d9f980b40c5dd64fc5b7a2
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# サポート通知にチームメンバーを含める方法

この記事では、チームメンバーを追加して、メール通知でサポートのアップデートを自動的に受信する方法について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [ サポート対象バージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)。

## 原因：

* チーム メンバーが必要な特権で [!DNL cloud project] に追加されていません。
* チームメンバーにサポートアカウントがありません。

## 解決策

1. **[!DNL Cloud Project URL]** に移動します（例：`https://us-3.magento.cloud/projects/xxxxxx/edit`）。
1. チームメンバーがプロジェクトに追加されたかどうか、および [!DNL Super User] ーザーであるかどうかを確認します。

[!DNL cloud project] のアクセスが必要ない場合は、[Adobe Commerce サポートセンターでのサポートリクエスト ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) を送信して、すべてのチケットで自動的に CC：を実行し、**[!DNL MAGE ID]** ールも提供します（利用可能な場合）。

アセットがプロジェクトに追加されていない場合は、アセットを [!DNL Super User] として追加し、[!DNL Shared Access] の権限を付与する必要があります。

* ユーザーガイドの [ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html)。
* Commerce ナレッジベースの [Adobe Commerce クラウドプロジェクトにユーザーを追加できない ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/unable-add-user-adobe-commerce-cloud-project.html)。
* [Adobe Commerce ヘルプセンターユーザーガイド：共有アクセス ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access) （Commerce ナレッジベース）。

ユーザーが [!DNL cloud project] に追加されたが、[!DNL Super User role] がない場合、[ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html) で適切に [!DNL role] を更新します。

## 関連資料

[ 以前のチームメンバーには、Adobe Commerce Cloud 通知メールが届きます ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/former-teammembers-receive-cloud-notification-emails.html)
