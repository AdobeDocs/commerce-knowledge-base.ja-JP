---
title: 以前のチームメンバーがAdobe Commerce cloud通知メールを受信する
description: この記事では、以前のチームメンバーに送信されるAdobe Commerce オンクラウドインフラストラクチャ通知メールに対する解決策を提供します。
exl-id: b2535f66-8aec-4ddf-9a69-60879a0a1939
feature: Cloud, Communications, Paas
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: bb03f6c4-cab9-560e-9d02-5816e1808d17
    internal-label: Communications
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
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
* 方法2: magento-cloud [!DNL CLI]を使用する 手順については、「Commerce on cloud infrastructure ガイド」の「 [!DNL CLI]&#x200B;[&#128279;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#manage-users-with-the-cli) ユーザーを使用してユーザーを管理する」を参照してください。

これが既に完了していて、そのユーザーがメール通知に引き続き含まれている場合は、サポートチケットを送信して、アカウントの&#x200B;*[!UICONTROL Always CC]*&#x200B;設定から削除するようにリクエストします。

## 関連トピックス

* [&#x200B; ユーザーのプロジェクトの役割](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html?lang=ja#view-a-user's-project-role)をCommerce on cloud infrastructure ガイドでご覧ください。
* [Commerce KBのサポート通知](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-include-a-team-member-in-support-notifications.html?lang=ja)にチームメンバーを含める方法。
