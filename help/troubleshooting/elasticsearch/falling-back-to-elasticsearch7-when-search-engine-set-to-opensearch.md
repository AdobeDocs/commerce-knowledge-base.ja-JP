---
title: 検索エンジンが [!DNL Opensearch]に設定されたときに [!DNL Elasticsearch7] にフォールバックします
description: この記事では、*Adobe Commerceで [!DNL Elasticsearch7]* error occurs when the search engine is set to [!DNL OpenSearch] にフォールバックする際の問題に対する解決策を提供します。
feature: Search
role: Developer
exl-id: 965d2929-5cf0-4e0a-9eed-6a656daaa120
source-git-commit: 40766238a7ea748bff86decf75cddec28fe63bb9
workflow-type: tm+mt
source-wordcount: '202'
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
