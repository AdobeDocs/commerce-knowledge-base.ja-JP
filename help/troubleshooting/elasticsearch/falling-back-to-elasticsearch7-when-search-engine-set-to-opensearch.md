---
title: 検索エンジンが[!DNL Opensearch]に設定されたときに[!DNL Elasticsearch7]にフォールバックします
description: この記事では、Adobe Commerceで検索エンジンが[!DNL OpenSearch]に設定されている場合に「[!DNL Elasticsearch7]*にフォールバック中」エラーが発生する場合の問題の解決策を紹介します。
feature: Search
role: Developer
exl-id: 965d2929-5cf0-4e0a-9eed-6a656daaa120
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%
---
# 検索エンジンが[!DNL Opensearch]に設定されたときに[!DNL Elasticsearch7]にフォールバックします

この記事では、Adobe Commerceで検索エンジンが[!DNL OpenSearch]に設定されている場合に&#x200B;*Falling back to[!DNL Elasticsearch7]* エラーが発生した場合の問題の解決策を紹介します。

## 影響のあるバージョン

Adobe Commerce on cloud infrastructure
2.4.4 - 2.4.4-p12
2.4.5 - 2.4.5-p11

>[!NOTE]
>
>[!DNL OpenSearch]は、Adobe Commerce 2.4.6、2.4.5-p12、2.4.4-p13以降の検索エンジンとして利用できます。

## イシュー

**検索エンジン**&#x200B;を&#x200B;**[!DNL OpenSearch]**&#x200B;に設定しましたが、`var/log/support_report.log` ファイルでこの種類のエラーを確認してください：

`[2024-04-04T00:27:41.212916+00:00] report.ERROR: opensearch search engine doesn't exist. Falling back to elasticsearch7 [] []`

<u>複製する手順</u>:

1. 次のコマンドを実行して、[!DNL OpenSearch]がインストールされていることを確認します。 `curl 127.0.0.1:9200`<br>
*1.2.4*&#x200B;を示す場合、[!DNL OpenSearch]は既にインストールされています。
1. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog Search]**&#x200B;に移動します。
1. 検索エンジンをチェック。 [!DNL Elasticsearch7]が表示されます。

## 原因

お使いのバージョンは[!DNL OpenSearch]をサポートしていますが、アプリケーションは[!DNL Elasticsearch7]を検索エンジンとしてのみ認識/承認します。

Adobe Commerce バージョン 2.4.6以降、アプリケーションが更新され、[!DNL OpenSearch]が検索エンジンとして選択できるようになりました。
クラウド以外の環境で**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog Search]**&#x200B;に移動すると、以下の&#x200B;**解決策**に示すように、このオプションを変更できます。
（注：クラウド環境では、検索エンジンが`app/etc/env.php` ファイルでロックされているため、このフィールドを変更することはできません）。

## Solution

`.magento.env.yaml` ファイルの`SEARCH_CONFIGURATION`変数を更新し、**検索エンジン**&#x200B;が&#x200B;*[!DNL elasticsearch7]*&#x200B;に設定されていることを確認します。

## 関連トピックス

Commerce on Cloud Infrastructure ガイドの[OpenSearch サービスの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/opensearch.html)。
