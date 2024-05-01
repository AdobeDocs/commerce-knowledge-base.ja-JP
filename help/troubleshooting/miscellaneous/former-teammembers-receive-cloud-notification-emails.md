---
title: 以前のチームメンバーには、Adobe Commerce クラウド通知メールが届きます
description: この記事では、以前のチームメンバーに送信される、クラウドインフラストラクチャ上のAdobe Commerceの通知メールに対するソリューションを説明します。
exl-id: b2535f66-8aec-4ddf-9a69-60879a0a1939
feature: Cloud, Communications, Paas
role: Developer
source-git-commit: 075f295c5b600fcca9fbecc5aad20b0640d900f9
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 以前のチームメンバーには、Adobe Commerce クラウド通知メールが届きます

この記事では、プロジェクトに関連付けられていないチームメンバーが、引き続き通知を受信する場合の解決策を提供します。

## 問題

検出された停電またはクラウドプロジェクト/環境に関する重要な問題の通知がチームに送信されました。 これには、外部/エージェンシー開発者やシステムインテグレーターなど、プロジェクトに関連付けられていないメンバーが含まれます。 これらのユーザーに通知の受信を停止する。

## 解決策

プロジェクトからユーザーを削除して通知を停止するには、次の 2 つの方法があります。

* 方法 1：クラウドの使用 [!DNL Project URL]. こちらを参照してください [ユーザーアクセスの管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html) 手順については、クラウドインフラストラクチャー上のCommerce ガイドを参照してください。
* 方法 2:magento-cloud の使用 [!DNL CLI]. こちらを参照してください [を使用したユーザー管理 [!DNL CLI]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html#manage-users-with-the-cli) 手順については、クラウドインフラストラクチャー上のCommerce ガイドを参照してください。

この操作が既に実行されているのに、これらのユーザーが引き続きメール通知に含まれる場合は、サポートチケットを送信して、 *[!UICONTROL Always CC]* アカウントの設定。

## 関連資料

* [ユーザーのプロジェクトの役割を表示する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/user-access.html#view-a-user&#39;s-project-role) （クラウドインフラストラクチャーに関するCommerceのガイド）を参照してください。
* [サポート通知にチームメンバーを含める方法](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-include-a-team-member-in-support-notifications.html) （Commerce KB 内）
