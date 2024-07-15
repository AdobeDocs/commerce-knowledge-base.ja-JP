---
title: 新規設定のチェックリスト  [!DNL domain]
description: これは、クラウドインフラストラクチャー上に新しいAdobe Commerceをセットアップする方法を  [!DNL domain]  すチェックリストです。
exl-id: bfe0582d-2c6d-4814-908f-dfd8c898bef7
feature: Cache
source-git-commit: 625ed2c7ab79f7bca9a979903e97c44c875e607c
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 新しい [!DNL domain] の設定のチェックリスト

これは、クラウドインフラストラクチャー上のAdobe Commerceで新しい [!DNL domain] を設定する方法を示したチェックリストです。 これは、新しいドメインを追加しようとしているか、現在のドメインを新しいドメインに置き換えようとしているかに関係なく適用されます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce[ サポート対象のすべてのバージョン ](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 新しいドメインの設定方法

### 手順 1 - [!DNL Integration, Staging] 用ですか、[!DNL Production environment] 用ですか。

* **[!DNL Integration]**: [!DNL Custom domains] はサポートされていません。 ユーザーガイドでは、この方法を代わりに使用する必要があります。[ 複数の web サイトまたはストアを設定する：ローカルインストールを設定する ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html#add-new-domains)。
* **[!DNL Staging]**: **手順 2** に移動します。
* **[!DNL Production]**: **手順 3** に移動します。

### 手順 2 - [!DNL Staging environment]:[!DNL Pro] または [!DNL Starter] を使用していますか？

* **[!DNL Pro]**: **リクエストを送信** してドメインを [!DNL Fastly, Nginx] に追加し、[!DNL SSL certificate] を設定（必要に応じて [!DNL Sendgrid domain] も設定）。 設定が完了したら、[ [!DNL development settings]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings) を使用して  [!DNL DNS]  設定を更新します。

>[!NOTE]
>
>ユーザーガイドの [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html#manage-domains) に [!DNL Fastly] すように、**[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Advanced]**/**[!UICONTROL System]**/**[!UICONTROL Full Page Cache]**/**[!DNL Fastly Configuration]**/**[!UICONTROL Domains]** の [!DNL Admin] で設定を更新することで、新しい [!DNL domain] を自分に追加できます。
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
>ユーザーガイドの **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Advanced]**/**[!UICONTROL System]**/**[!UICONTROL Full Page Cache]**/**[!DNL Fastly Configuration]**/**[!UICONTROL Domains]** [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html#manage-domains) の [!DNL Admin] で設定を更新することで、新しい [!DNL domain] を自分に追加で [!DNL Fastly] ます。
>
>
>ドメインを追加できない場合、次のいずれかの理由が原因である可能性があります。
>
>1. ドメインをオンプレミスからクラウド環境に移行しようとしています。この環境は、独自の [!DNL Fastly] サービスで構成されています。 この場合は、リクエストを送信し、ドメインのデリゲーションをリクエストします。
>1. ドメインを Starter から Pro に移行します。 この場合は、さらに支援を求める要求を送信します。

* **[!DNL Starter]**:「リク [!DNL domain] スト」タブでプロジェクトにリク **[!DNL Domains]** ストを追加し、**リクエストを送信** してリク [!DNL SSL certificate] ストの **[!DNL ACME Challenge Key]** を指定します。

### 手順 4 - [!DNL domain] はライブですか？

* **はい**: [[!UICONTROL production] 設定で  [!DNL DNS]  設定を更新 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html#update-dns-configuration-with-production-settings)。
* **いいえ**: [[!UICONTROL development] 設定で  [!DNL DNS]  設定を更新 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings)。

## 関連資料

* ユーザーガイドの [ 複数の web サイトまたはストアを設定：新規追加  [!DNL Domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html#add-new-domains)。
