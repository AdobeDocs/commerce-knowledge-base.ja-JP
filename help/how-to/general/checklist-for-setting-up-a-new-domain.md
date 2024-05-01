---
title: 新規設定のチェックリスト [!DNL domain]
description: これは、新規設定方法のチェックリストです。 [!DNL domain] クラウドインフラストラクチャー上のAdobe Commerceで。
exl-id: bfe0582d-2c6d-4814-908f-dfd8c898bef7
feature: Cache
source-git-commit: cc3dc1e3f9c8f98370ce5db125b402d4c1dfbd6f
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 新規設定のチェックリスト [!DNL domain]

これは、新規設定方法のチェックリストです。 [!DNL domain] クラウドインフラストラクチャー上のAdobe Commerceで。 これは、新しいドメインを追加しようとしているか、現在のドメインを新しいドメインに置き換えようとしているかに関係なく適用されます。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 新しいドメインの設定方法

### 手順 1 – このは [!DNL Integration, Staging]、または [!DNL Production environment]?

* **[!DNL Integration]**: [!DNL Custom domains] はサポートされていません。 代わりに、次の方法を使用する必要があります。 [複数の web サイトまたはストアの設定：ローカルインストールの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html#add-new-domains) を参照してください。
* **[!DNL Staging]**：に移動します **手順 2**.
* **[!DNL Production]**：に移動します **手順 3**.

### 手順 2 - [!DNL Staging environment]：を担当しています [!DNL Pro] または [!DNL Starter]?

* **[!DNL Pro]**: **リクエストの送信** ドメインの追加先 [!DNL Fastly, Nginx]を作成し、を設定します [!DNL SSL certificate] （および [!DNL Sendgrid domain]（必要に応じて）。 設定が完了したら、 [を更新 [!DNL DNS] を使用した設定 [!DNL development settings]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings).

>[!NOTE]
>
>新しいを追加できます [!DNL domain] 対象： [!DNL Fastly] で設定を更新することにより、自分で行うことができます。 [!DNL Admin] 。対象： **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Full Page Cache]** > **[!DNL Fastly Configuration]** > **[!UICONTROL Domains]** 例： [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html#manage-domains) を参照してください。

* **[!DNL Starter]**: [!DNL Custom domains] はサポートされていません。

### 手順 3 - [!DNL Production environment]：を担当しています [!DNL Pro] または [!DNL Starter]?

* **[!DNL Pro]**: **リクエストの送信** ドメインの追加先 [!DNL Fastly, Nginx]を作成し、を設定します [!DNL SSL certificate] （例： [!DNL Sendgrid domain]（必要に応じて）。 設定が完了したら、次に進みます。 **手順 4**.

>[!NOTE]
>
>新しいを追加できます [!DNL domain] 対象： [!DNL Fastly] で設定を更新することにより、自分で行うことができます。 [!DNL Admin] 。対象： **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Full Page Cache]** > **[!DNL Fastly Configuration]** > **[!UICONTROL Domains]** [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html#manage-domains) を参照してください。

* **[!DNL Starter]**：を追加 [!DNL domain] をプロジェクトに追加する **[!DNL Domains]** タブをクリックし、 **リクエストの送信** を提供する **[!DNL ACME Challenge Key]** の場合 [!DNL SSL certificate].

### 手順 4 – は [!DNL domain] ライブ？

* **はい**: [を更新 [!DNL DNS] を使用した設定 [!UICONTROL production] 設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html#update-dns-configuration-with-production-settings).
* **不可**: [を更新 [!DNL DNS] を使用した設定 [!UICONTROL development] 設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings).

## 関連資料

* [複数の web サイトまたはストアの設定：新規追加 [!DNL Domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html#add-new-domains) を参照してください。
