---
title: 新規設定のチェックリスト  [!DNL domain]
description: これは、クラウドインフラストラクチャー上に新しいAdobe Commerceをセットアップする方法を  [!DNL domain]  すチェックリストです。
exl-id: bfe0582d-2c6d-4814-908f-dfd8c898bef7
feature: Cache
source-git-commit: f7b246088e3580922bd3389b2992e5dd8f97ff7a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 新しい [!DNL domain] の設定のチェックリスト

このチェックリストでは、クラウドインフラストラクチャ上のAdobe Commerceで新しい [!DNL domain] を設定する方法について説明します。 これは、新しいドメインを追加する場合でも、現在のドメインを置き換える場合でも適用されます。 これは、新しいステージング環境を取得した後にも適用されます（手順 4 を参照）。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 新しいドメインの設定方法

### 手順 1 - [!DNL Integration, Staging] 用ですか、[!DNL Production environment] 用ですか。

* **[!DNL Integration]**: [!DNL Custom domains] はサポートされていません。 ユーザーガイドでは、この方法を代わりに使用する必要があります。[ 複数の web サイトまたはストアを設定する：ローカルインストールを設定する ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html?lang=ja#add-new-domains)。
* **[!DNL Staging]**: **手順 2** に移動します。
* **[!DNL Production]**: **手順 3** に移動します。

### 手順 2 - [!DNL Staging environment]:[!DNL Pro] または [!DNL Starter] を使用していますか？

* **[!DNL Pro]**: **リクエストを送信** してドメインを [!DNL Fastly, Nginx] に追加し、[!DNL SSL certificate] を設定（必要に応じて [!DNL Sendgrid domain] も設定）。 設定が完了したら、[ [!DNL development settings]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja#update-dns-configuration-with-development-settings) を使用して  [!DNL DNS]  設定を更新します。

>[!NOTE]
>
>ユーザーガイドの [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html?lang=ja#manage-domains) に [!DNL Fastly] すように、**[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Advanced]**/**[!UICONTROL System]**/**[!UICONTROL Full Page Cache]**/**[!DNL Fastly Configuration]**/**[!UICONTROL Domains]** の [!DNL Admin] で設定を更新することで、新しい [!DNL domain] を自分に追加できます。
>
>ドメインを追加できない場合、次のいずれかの理由が原因である可能性があります。
>
>1. 独自の [!DNL Fastly] サービスに設定されたクラウド環境にドメインを移行しようとしています。 この場合は、リクエストを送信し、ドメインのデリゲーションをリクエストします。
>1. ドメインを Starter から Pro に移行します。 この場合は、さらに支援を求める要求を送信します。

* **[!DNL Starter]**: [!DNL Custom domains] はステージング環境ではサポートされていません。

### 手順 3 - [!DNL Production environment]:[!DNL Pro] または [!DNL Starter] を使用していますか？

* **[!DNL Pro]**: **リクエストを送信** してドメインを [!DNL Fastly, Nginx] に追加し、[!DNL SSL certificate] を（必要に応じて [!DNL Sendgrid domain] として）設定します。 設定が完了したら、**手順 4** に進みます。

>[!NOTE]
>
>ユーザーガイドの **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Advanced]**/**[!UICONTROL System]**/**[!UICONTROL Full Page Cache]**/**[!DNL Fastly Configuration]**/**[!UICONTROL Domains]** [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html?lang=ja#manage-domains) の [!DNL Admin] で設定を更新することで、新しい [!DNL domain] を自分に追加で [!DNL Fastly] ます。
>
>
>ドメインを追加できない場合、次のいずれかの理由が原因である可能性があります。
>
>1. ドメインをオンプレミスからクラウド環境に移行しようとしています。この環境は、独自の [!DNL Fastly] サービスで構成されています。 この場合は、リクエストを送信し、ドメインのデリゲーションをリクエストします。
>1. ドメインを Starter から Pro に移行します。 この場合は、さらに支援を求める要求を送信します。

* **[!DNL Starter]**:「リク [!DNL domain] スト」タブでプロジェクトにリク **[!DNL Domains]** ストを追加し、**リクエストを送信** してリク [!DNL SSL certificate] ストの **[!DNL ACME Challenge Key]** を指定します。

### 手順 4 - [!DNL domain] はライブですか？

* **はい**: [[!UICONTROL production] 設定で  [!DNL DNS]  設定を更新 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html?lang=ja#update-dns-configuration-with-production-settings)。
* **いいえ**: [[!UICONTROL development] 設定で  [!DNL DNS]  設定を更新 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja#update-dns-configuration-with-development-settings)。

## 関連資料

* ユーザーガイドの [ 複数の web サイトまたはストアを設定：新規追加  [!DNL Domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html?lang=ja#add-new-domains)。
* [ 接触チャネルクロークによりサイトにアクセスできない ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/site-down-or-unresponsive/production-site-not-accessible-due-to-origin-cloaking)
