---
title: MBI：統合の再認証
description: この記事では、サードパーティのサービスからデータを取り込むために必要な権限を Magento Business Intelligence （MBI）に付与するために、統合を再認証するソリューションを提供します。 これらの権限が取り消された場合は、再認証が必要です。
exl-id: c608d6f9-64a5-44f8-9d7b-9a85a2668775
feature: Commerce Intelligence, Integration
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# MBI：統合の再認証

この記事では、サードパーティのサービスからデータを取り込むために必要な権限を Magento Business Intelligence （MBI）に付与するために、統合を再認証するソリューションを提供します。 これらの権限が取り消された場合は、再認証が必要です。

## データベースと SaaS の統合

データベースおよび SaaS 統合のリストについては、開発者向けドキュメントの [&#x200B; 統合を使用した外部データの接続 &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-business-intelligence/mbi/analyze/saas/integrations) を参照してください。 （ページを開く場合は、左側の目次をナビゲーションに使用します）。

## 接続に問題がありますか？

統合を承認すると、サードパーティのサービスからデータを取り込むために必要な権限が MBI に付与されます。 これらの権限が取り消された場合は、再認証が必要です。

これは、次のようないくつかの理由で発生する可能性があります。

* サードパーティサービスの問題
* 認証トークンの有効期限
* 管理者アカウントに加えられた変更
* または MBI 内の内部問題

すべての統合のステータスは統合ページ（**データを管理/統合**）に表示されます。

![Integrations_page.png](assets/Integrations_page.png)

再認証するには、アカウント資格情報を再入力する必要がある場合があります。 場合によっては、問題を統合するために新しい API キーの生成が必要になることもあります。 問題の統合の名前をクリックして、再認証プロセスを開始します。

問題が解決しない場合は、[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) してください。
