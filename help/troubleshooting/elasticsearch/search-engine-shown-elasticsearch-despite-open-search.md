---
title: '[!DNL Elasticsearch] にもかかわらず検索エンジンとして表示される [!DNL OpenSearch] インストール'
description: この記事では、次の問題の解決策について説明します [!DNL Elasticsearch] をインストールまたはアップグレードした後でも、が cloud 上のAdobe Commerceの検索エンジンとして引き続き表示されます。 [!DNL OpenSearch].
exl-id: cdd8a35d-da6f-46d3-b732-65626487c9bb
feature: Install
source-git-commit: 1f053f76ae56edc06bfe82e55210244c8ec4b8eb
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# [!DNL Elasticsearch] にもかかわらず検索エンジンとして表示される [!DNL OpenSearch] インストール

この記事では、次の問題の解決策について説明します [!DNL Elasticsearch] をインストールまたはアップグレードした後でも、が cloud 上のAdobe Commerceの検索エンジンとして引き続き表示されます。 [!DNL OpenSearch].

## 影響を受けるバージョン

cloud 2.4.3-p2 - 2.4.5-p6 のAdobe Commerce

>[!NOTE]
>
>[!DNL OpenSearch] は、Adobe Commerce 2.4.6 以降の検索エンジンとして使用できます。

## 問題

[!DNL Elasticsearch] をインストールまたはアップグレードした後でも、が cloud 上のAdobe Commerceの検索エンジンとして引き続き表示されます。 [!DNL OpenSearch].

<u>再現手順</u>:

1. に移動 **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Catalog]** > **[!UICONTROL Catalog Search]**.
1. 検索エンジンを確認します。 次の内容が表示されます [!DNL Elasticsearch7].

## 原因：

Adobe Commerceは、を指定するようにハードコードされています [!DNL Elasticsearch7] を検索エンジンとして使用します。

これは、インストールされているバージョンのサービスと混同しないでください。 アプリケーションが認識するのは [!DNL Elasticsearch7] を検索エンジンとして使用しますが、は使用しません [!DNL OpenSearch]を使用する場合でも [!DNL OpenSearch] バックエンドのエンジンとしてのサービス。

## 解決策

次のかどうかを確認します [!DNL OpenSearch] がインストールされている場合は、次のコマンドを実行します。

**方法 1**:

* サーバーで次のコマンドを実行します。 `curl 127.0.0.1:9200`. が返されます [!DNL OpenSearch] とそのバージョン。

例：

```
$ curl 127.0.0.1:9200
{
  "name" : $clusterName,
  "cluster_name" : "opensearch_stg",
  "cluster_uuid" : $clusterUuid,
  "version" : {
    "distribution" : "opensearch",
    "number" : "1.2.4",
    "build_type" : "deb",
    "build_hash" : "44ccdbaed5fe5a8b02d99a611857a671b6dd909d",
    "build_date" : "2022-11-08T09:23:45.993372Z",
    "build_snapshot" : false,
    "lucene_version" : "8.10.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "The OpenSearch Project: https://opensearch.org/"
}
```

**方法 2**:

* Magentoクラウド CLI で次のコマンドを使用します。 `magento-cloud relationships -p <project_id>`. コマンドを使用して、次を見つけます [!DNL OpenSearch].

## 関連資料

[OpenSearch サービスの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/opensearch.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。
