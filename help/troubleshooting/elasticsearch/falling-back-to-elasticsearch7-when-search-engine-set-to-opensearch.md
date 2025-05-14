---
title: 検索エンジンがに設定されている場合に  [!DNL Elasticsearch7]  フォールバック  [!DNL Opensearch]
description: この記事では、Adobe Commerceでのフォールバック時の問題のソリューショ  [!DNL Elasticsearch7]* error occurs when the search engine is set to [!DNL OpenSearch]  を説明します。
feature: Search
role: Developer
exl-id: 965d2929-5cf0-4e0a-9eed-6a656daaa120
source-git-commit: d17af0f8f92726aa5a6914fc9e1ff13268256d04
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 検索エンジンが [!DNL Opensearch] に設定されている場合に [!DNL Elasticsearch7] にフォールバック

この記事では、Adobe Commerceで検索エンジンが「[!DNL OpenSearch]」に設定されている場合に *[!DNL Elasticsearch7]* のエラーにフォールバックする」と表示される問題の解決策について説明します。

## 影響を受けるバージョン

クラウドインフラストラクチャー上のAdobe Commerce
2.4.4 - 2.4.4-p12
2.4.5 - 2.4.5-p11

>[!NOTE]
>
>[!DNL OpenSearch] は、Adobe Commerce 2.4.6、2.4.5-p12、2.4.4-p13 以降の検索エンジンとして使用できます。

## 問題

**検索エンジン** を **[!DNL OpenSearch]** に設定しましたが、`var/log/support_report.log` ファイルにこのタイプのエラーが表示されます。

```[2024-04-04T00:27:41.212916+00:00] report.ERROR: opensearch search engine doesn't exist. Falling back to elasticsearch7 [] []```

<u> 再現手順 </u>:

1. 次のコマンドを実行して、[!DNL OpenSearch] がインストールされていることを確認します：`curl 127.0.0.1:9200`<br>
*1.2.4* と表示される場合は、[!DNL OpenSearch] は既にインストールされています。
1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Catalog Search]** に移動します。
1. 検索エンジンを確認します。 [!DNL Elasticsearch7] が表示されます。

## 原因：

お使いのバージョンが [!DNL OpenSearch] をサポートしている場合でも、アプリケーションは [!DNL Elasticsearch7] を検索エンジンとして認識または承認するだけです。

Adobe Commerce バージョン 2.4.6 以降、[!DNL OpenSearch] を検索エンジンとして選択できるように更新されました。
クラウド以外の環境で **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Catalog Search]** に移動すると、以下の **ソリューション** に示すように、このオプションを変更できます。
（メモ：クラウド環境では、検索エンジンが `app/etc/env.php` ファイルでロックされているので、このフィールドは変更できません。）

## 解決策

`.magento.env.yaml` ファイルの `SEARCH_CONFIGURATION` 変数を更新し、**検索エンジン** が *[!DNL elasticsearch7]* に設定されていることを確認します。

## 関連資料

Commerce on Cloud Infrastructure ガイドの [OpenSearch サービスの設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/opensearch.html?lang=ja)。
