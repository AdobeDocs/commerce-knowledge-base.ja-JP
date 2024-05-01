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

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [サポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf).

## 原因：

* チームメンバーがに追加されていません [!DNL cloud project] 必要な権限を持つ。
* チームメンバーにサポートアカウントがありません。

## 解決策

1. に移動します **[!DNL Cloud Project URL]** （例： `https://us-3.magento.cloud/projects/xxxxxx/edit`）に設定します。
1. チームメンバーがプロジェクト（）に追加されたかどうかを確認する [!DNL Super User].

必要なければ、 [!DNL cloud project] アクセス、送信 [Adobe Commerce サポートセンターでのサポートリクエスト](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) 自動的に CC するには：すべてのチケットでそれらを提供します **[!DNL MAGE ID]** （使用可能な場合）。

プロジェクトに追加されていない場合は、として追加する必要があります [!DNL Super User] とグラント [!DNL Shared Access]:

* [ユーザーアクセスの管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html) を参照してください。
* [Adobe Commerce クラウドプロジェクトにユーザーを追加できない](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/unable-add-user-adobe-commerce-cloud-project.html) Commerceのナレッジベースで。
* [Adobe Commerce ヘルプセンターユーザーガイド：共有アクセス](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access) Commerceのナレッジベースで。

に追加されている場合 [!DNL cloud project]ただし、次の権限はありません [!DNL Super User role]、を更新 [!DNL role] それに応じて [ユーザーアクセスの管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html).

## 関連資料

[以前のチームメンバーには、Adobe Commerce クラウド通知メールが届きます](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/former-teammembers-receive-cloud-notification-emails.html)
