---
title: 以前のチームメンバーがAdobe Commerce cloud通知メールを受信する
description: この記事では、以前のチームメンバーに送信されるAdobe Commerce オンクラウドインフラストラクチャ通知メールに対する解決策を提供します。
exl-id: b2535f66-8aec-4ddf-9a69-60879a0a1939
feature: Cloud, Communications, Paas
role: Developer
source-git-commit: bd199fac6d8f33491b9fa0f508b2bb52d56b46a5
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 以前のチームメンバーがAdobe Commerce cloud通知メールを受信する

この記事では、次のユーザーを受信者の通知メールのリストからユーザーを削除するためのソリューションを提供します。

* プロジェクトに関連付けられなくなった以前のチームメンバー。
* 通知を受信しない現在のチームメンバー。

## イシュー

クラウドプロジェクト/環境に関して、検出された停止または重要な問題に関する通知がチームに送信されました。 これには、外部/代理店の開発者やシステムインテグレーターなど、プロジェクトに関連付けられなくなったメンバーが含まれます。 これらのユーザーに通知の受信を停止する必要があります。

## Solution

>[!NOTE]
>
>外部/代理店の開発者またはシステムインテグレーターで、プロジェクトに関連付けられなくなった場合は、そのプロジェクトのプロジェクトオーナーまたはプロジェクト管理者に連絡してサポートを受ける必要があります。

ユーザーをプロジェクトから削除して、通知を停止するには、次の2つの方法があります。

* 方法1: クラウド [!DNL Project URL]を使用する。 手順については、『Commerce on cloud infrastructure ガイド』の「[&#x200B; ユーザーアクセスの管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja)」を参照してください。
* 方法2: magento-cloud [!DNL CLI]を使用する 手順については、「Commerce on cloud infrastructure ガイド」の「 [!DNL CLI][&#128279;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#manage-users-with-the-cli) ユーザーを使用してユーザーを管理する」を参照してください。

これが既に完了していて、そのユーザーがメール通知に引き続き含まれている場合は、サポートチケットを送信して、アカウントの&#x200B;*[!UICONTROL Always CC]*&#x200B;設定から削除するようにリクエストします。

## 関連トピックス

* [&#x200B; ユーザーのプロジェクトの役割](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#view-a-user's-project-role)をCommerce on cloud infrastructure ガイドでご覧ください。
* [Commerce KBのサポート通知](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-include-a-team-member-in-support-notifications.html?lang=ja)にチームメンバーを含める方法。
