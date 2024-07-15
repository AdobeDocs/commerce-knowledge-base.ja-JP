---
title: 「[!DNL Elasticsearch] はインストールに関係なく検索エンジンと  [!DNL OpenSearch]  て表示されます」
description: この記事では、 [!DNL OpenSearch] をインストールまたはアップグレードした後も  [!DNL Elasticsearch] cloud 上のAdobe Commerceの検索エンジンとして引き続き表示される問題の解決策を説明します。
exl-id: cdd8a35d-da6f-46d3-b732-65626487c9bb
feature: Install
source-git-commit: 1f053f76ae56edc06bfe82e55210244c8ec4b8eb
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# インストールに関係なく、検索エンジンとして [!DNL Elasticsearch] が表示 [!DNL OpenSearch] れます

この記事では、[!DNL OpenSearch] をインストールまたはアップグレードした後も [!DNL Elasticsearch] が cloud 上のAdobe Commerceの検索エンジンとして引き続き表示される問題の解決策について説明します。

## 影響を受けるバージョン

cloud 2.4.3-p2 - 2.4.5-p6 のAdobe Commerce

>[!NOTE]
>
>[!DNL OpenSearch] は、Adobe Commerce 2.4.6 以降で検索エンジンとして使用できます。

## 問題

[!DNL Elasticsearch] をインストールした後や [!DNL OpenSearch] にアップグレードした後でも、cloud 上のAdobe Commerceの検索エンジンとして引き続き表示されます。

<u> 再現手順 </u>:

1. **[!UICONTROL Stores]**/**[!UICONTROL Configuration]**/**[!UICONTROL Catalog]**/**[!UICONTROL Catalog Search]** に移動します。
1. 検索エンジンを確認します。 [!DNL Elasticsearch7] が表示されます。

## 原因：

Adobe Commerceは、検索エンジンとして [!DNL Elasticsearch7] を指定するようにハードコードされています。

これは、インストールされているバージョンのサービスと混同しないでください。 基になる [!DNL OpenSearch] サービスをバックエンドのエンジンとして使用しているにもかかわらず、アプリケーションは [!DNL Elasticsearch7] を検索エンジンとして認識するだけで、[!DNL OpenSearch] は認識しません。

## 解決策

[!DNL OpenSearch] がインストールされているかどうかを確認するには、次のコマンドを実行します。

**メソッド 1**:

* サーバーで次のコマンドを実行します：`curl 127.0.0.1:9200`。 バージョンと共に [!DNL OpenSearch] が返されます。

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

**メソッド 2**:

* Magentoクラウド CLI で、`magento-cloud relationships -p <project_id>` コマンドを使用します。 コマンドを使用して、[!DNL OpenSearch] を見つけます。

## 関連資料

Commerce on Cloud Infrastructure ガイドの [OpenSearch サービスの設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/opensearch.html)。
