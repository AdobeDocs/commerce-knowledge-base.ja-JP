---
title: 以前のチームメンバーには、Adobe Commerce クラウド通知メールが届きます
description: この記事では、以前のチームメンバーに送信される、クラウドインフラストラクチャ上のAdobe Commerceの通知メールに対するソリューションを説明します。
exl-id: b2535f66-8aec-4ddf-9a69-60879a0a1939
feature: Cloud, Communications, Paas
role: Developer
source-git-commit: bd199fac6d8f33491b9fa0f508b2bb52d56b46a5
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 以前のチームメンバーには、Adobe Commerce クラウド通知メールが届きます

この記事では、次のユーザーを受信者の通知メールのリストから削除するソリューションを提供します。

* 以前のチームメンバーで、プロジェクトとの関連付けがなくなった人。
* 通知を受け取るべきではない現在のチームメンバー。

## 問題

検出された停電またはクラウドプロジェクト/環境に関する重要な問題の通知がチームに送信されました。 これには、外部/エージェンシー開発者やシステムインテグレーターなど、プロジェクトに関連付けられていないメンバーが含まれます。 これらのユーザーに通知の受信を停止する。

## 解決策

>[!NOTE]
>
>外部/エージェンシー開発者またはシステムインテグレーターで、プロジェクトとの関連付けが終了した場合は、そのプロジェクトのプロジェクト所有者またはプロジェクト管理者に連絡してサポートを受ける必要があります。

プロジェクトからユーザーを削除して通知を停止するには、次の 2 つの方法があります。

* 方法 1:Cloud [!DNL Project URL] の使用。 手順については、クラウドインフラストラクチャー上のCommerce ガイドの [ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html) を参照してください。
* 方法 2:magento-cloud [!DNL CLI] の使用。 手順については、クラウドインフラストラクチャー上のCommerce ガイドの [ を使用したユーザーの管理  [!DNL CLI]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html#manage-users-with-the-cli) を参照してください。

この操作が既に実行されていて、さらにメール通知にこれらのユーザーが引き続き含まれる場合は、サポートチケットを送信して、アカウントの *[!UICONTROL Always CC]* 設定からユーザーを削除するようにリクエストします。

## 関連資料

* Commerce on cloud infrastructure ガイドの [ ユーザーのプロジェクトの役割を表示 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html#view-a-user&#39;s-project-role) します。
* Commerce KB で [ サポート通知にチームメンバーを含める方法 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-include-a-team-member-in-support-notifications.html)
