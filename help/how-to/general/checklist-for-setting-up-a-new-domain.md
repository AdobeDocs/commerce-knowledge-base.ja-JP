---
title: 新しい [!DNL domain]を設定するためのチェックリスト
description: これは、クラウドインフラストラクチャ上のAdobe Commerceで新しい [!DNL domain] を設定する方法のチェックリストです。
exl-id: bfe0582d-2c6d-4814-908f-dfd8c898bef7
feature: Cache
source-git-commit: 552a290b50f9e0c5fa740f26092c57bac447fe68
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# 新しい[!DNL domain]を設定するためのチェックリスト

このチェックリストでは、クラウドインフラストラクチャ上のAdobe Commerceで新しい[!DNL domain]を設定する方法について説明します。 新しいドメインを追加する場合でも、現在のドメインを置き換える場合でも適用されます。 新しいステージング環境を取得した後にも適用されます（手順4を参照）。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/Adobe-Commerce-Software-Lifecycle-Policy.pdf)

## 新しいドメインの設定方法

>[!NOTE]
>
>ドメインの設定に進む前に、次のことを確認してください。
>
>すべてのベース URLは、**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL General]** > **[!UICONTROL Web]**&#x200B;の下でHTTPSを使用するように設定されており、正しいweb サイトまたはストアビューを対象としています。
> [TLS](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls#token_type=bearer&expires_in=10799996)を強制的に有効にして、すべてのHTTP トラフィックをAdobe Commerce サイト全体のHTTPSにクラウドインフラストラクチャ上でリダイレクトします。

### 手順1 – これは[!DNL Integration, Staging]または[!DNL Production environment]用ですか？

* **[!DNL Integration]**: [!DNL Custom domains]はサポートされていません。 代わりに、この方法を使用する必要があります。[複数のWeb サイトまたはストアを設定する：ユーザーガイドのローカルインストール &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html?lang=ja#add-new-domains)を設定します。
* **[!DNL Staging]**: **手順2**&#x200B;に移動します。
* **[!DNL Production]**: **手順3**&#x200B;に移動します。

### 手順2 - [!DNL Staging environment]: [!DNL Pro]または[!DNL Starter]を使用していますか？

* **[!DNL Pro]**: **ドメインを[!DNL Fastly, Nginx]に追加するリクエスト**&#x200B;を送信し、[!DNL SSL certificate]を設定します（必要に応じて[!DNL Sendgrid domain]と同様）。 設定が完了したら、[で [!DNL DNS] 設定を [!DNL development settings]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja#update-dns-configuration-with-development-settings)に更新します。

>[!NOTE]
>
>PRO アーキテクチャの場合、新しいドメインを追加するには、サポートリクエストをAdobe Commerceに送信する必要があります。 一部のお客様は、Admin Consoleを介してFastlyを手動で設定できる場合がありますが、これは、ドメインが別のFastly サービスまたはプロジェクトに関連付けられていない場合など、限られた場合にのみ適用されます。 ただし、Nginx設定は常に必要であり、この手順はAdobeで処理する必要があります。 このため、推奨される最も信頼できる方法は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support)を送信し、Adobeにドメイン設定プロセス全体を管理させることです。


* **[!DNL Starter]**: [!DNL Custom domains]はステージング環境ではサポートされていません。

### 手順3 - [!DNL Production environment]: [!DNL Pro]または[!DNL Starter]を使用していますか？

* **[!DNL Pro]**: **ドメインを[!DNL Fastly, Nginx]に追加するリクエスト**&#x200B;を送信し、[!DNL SSL certificate]を設定します（必要に応じて[!DNL Sendgrid domain]として）。 設定が完了したら、**手順4**&#x200B;に進みます。

>[!NOTE]
>
>新しい[!DNL domain]を自分で[!DNL Fastly]に追加するには、ユーザーガイドの&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Full Page Cache]** > **[!DNL Fastly Configuration]** > **[!UICONTROL Domains]** [[!DNL Manage domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration.html?lang=ja#manage-domains)の[!DNL Admin]で設定を更新します。
>
>
>ドメインを追加できない場合は、次のいずれかの理由が考えられます。
>
>1. ドメインをオンプレミスからクラウド環境に移行しています。この環境は、独自の[!DNL Fastly] サービスで設定されています。 この場合は、ドメインのリクエストとリクエストの委任を送信します。
>1. StarterからProにドメインを移行しています。 この場合は、さらにサポートを依頼してください。

* **[!DNL Starter]**: [!DNL domain]を&#x200B;**[!DNL Domains]** タブのプロジェクトに追加し、**リクエストを送信**&#x200B;して[!DNL SSL certificate]に&#x200B;**[!DNL ACME Challenge Key]**&#x200B;を提供します。

### 手順4 - [!DNL domain]は公開されていますか？

* **YES**: [設定[!UICONTROL production]で [!DNL DNS] 設定を更新](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/checklist.html?lang=ja#update-dns-configuration-with-production-settings)。
* **NO**: [設定[!UICONTROL development]で [!DNL DNS] 設定を更新](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html?lang=ja#update-dns-configuration-with-development-settings)。

### 手順5 - ドメインリダイレクトは`magento-vars.php`で設定されていますか？

ドメインを設定したら、`magento-vars.php` ファイルの変数[&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/configure-store/multiple-sites#modify-variables)を変更して、ドメインを適切なweb サイト/ストア URLに誘導する必要があります。

### 手順6 - [!DNL domain]の設定は検証されますか？

新しいドメインの&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**&#x200B;に新しいストア、ストアグループ、およびweb サイトを追加した場合は、次のセクションが`app/etc/config.php` ファイルに表示されるかどうかを確認します（例：）。

```php
'scopes' => [
    'websites' => [
        'admin' => [
            'website_id' => '0',
            'code' => 'admin',
            'name' => 'Admin',
            'sort_order' => '0',
            'default_group_id' => '0',
            'is_default' => '0',
        ],
        'base' => [
            'website_id' => '1',
            'code' => 'base',
            'name' => 'Main Website',
            'sort_order' => '0',
            'default_group_id' => '1',
            'is_default' => '1',
        ],
        'site2' => [
            'website_id' => '2',
            'code' => 'site2',
            'name' => 'Second Website',
            'sort_order' => '0',
            'default_group_id' => '2',
            'is_default' => '0',
        ],
    ],
    'groups' => [
        0 => [
            'group_id' => '0',
            'website_id' => '0',
            'name' => 'Default',
            'root_category_id' => '0',
            'default_store_id' => '0',
            'code' => 'default',
        ],
        1 => [
            'group_id' => '1',
            'website_id' => '1',
            'name' => 'Main Website Store',
            'root_category_id' => '2',
            'default_store_id' => '1',
            'code' => 'main_website_store',
        ],
        2 => [
            'group_id' => '2',
            'website_id' => '2',
            'name' => 'Second Website Store',
            'root_category_id' => '2',
            'default_store_id' => '2',
            'code' => 'site2store',
        ],
    ],
    'stores' => [
        'admin' => [
            'store_id' => '0',
            'code' => 'admin',
            'website_id' => '0',
            'group_id' => '0',
            'name' => 'Admin',
            'sort_order' => '0',
            'is_active' => '1',
        ],
        'default' => [
            'store_id' => '1',
            'code' => 'default',
            'website_id' => '1',
            'group_id' => '1',
            'name' => 'Default Store View',
            'sort_order' => '0',
            'is_active' => '1',
        ],
        'site2sv' => [
            'store_id' => '2',
            'code' => 'site2sv',
            'website_id' => '2',
            'group_id' => '2',
            'name' => 'Second Website Store view',
            'sort_order' => '0',
            'is_active' => '1',
        ],
    ],
]
```

これは、過去に`ece-tools` パッケージで`config:dump` コマンドを実行して、ビルド [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-on-cloud/user-guide/develop/deploy/static-content#setting-the-scd-on-build)でSCDを設定したことがあることを意味します。

作成した新しいストアまたはweb サイトが`app/etc/config.php` ファイルに表示されていないことがわかった場合は、必ずコマンドを再実行して、`config.php` ファイルをデータベースへの変更と同期させ、`config.php` ファイルをコミットして再デプロイします。 これは、新しいストア/web サイトの適切なファイルパスへの静的コンテンツのデプロイメントを容易にするためです。

## 関連トピックス

* [複数のweb サイトまたはストアを設定する：新しい [!DNL Domains]](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites.html?lang=ja#add-new-domains)をユーザーガイドに追加します。
* [オリジンのクローク処理によりサイトにアクセスできません](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26856)
