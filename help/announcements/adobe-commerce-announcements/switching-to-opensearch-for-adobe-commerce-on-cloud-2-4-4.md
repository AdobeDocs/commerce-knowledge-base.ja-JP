---
title: Cloud 2.4.4 でのAdobe Commerceの OpenSearch への切り替え
promoted: true
description: クラウドインフラストラクチャー 2.4.4 上のAdobe Commerceでは、7.10 以降、Elasticsearchのバージョンをサポートしません。 **最初にAdobe Commerce 2.4.4 にアップグレードしてから、すぐにElasticsearch環境から OpenSearch 1.2.x.** Adobeに切り替える必要があります。このバージョンでは、Adobe Commerce 2.4.4 GA リリースに近い詳細な手順が提供されます。
exl-id: 0cb34cee-d4d9-428e-a7fd-7301a86dd8f6
feature: Cloud, Iaas, Paas, Search, Services
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Cloud 2.4.4 でのAdobe Commerceの OpenSearch への切り替え

クラウドインフラストラクチャー 2.4.4 上のAdobe Commerceでは、7.10 以降、Elasticsearchのバージョンをサポートしません。 **まずAdobe Commerce 2.4.4 にアップグレードしてから、すぐにElasticsearchから OpenSearch 1.2.x に切り替える必要があります。** Adobeでは、Adobe Commerce 2.4.4 GA リリースに近い詳細な手順を提供します。

>[!NOTE]
>
>切り替えは、クラウドプロバイダーに関係なく行う必要があります。

Adobe Commerce オンプレミスでは、2022 年 3 月のすべてのパッチリリース（2.4.4、2.4.3-p2、および 2.3.7-p3）で、Elasticsearch 7.16 と OpenSearch 1.2 のサポートが追加されています。 2.4.4 では、クラウドインフラストラクチャー上のAdobe Commerceがデフォルトの検索エンジンとして OpenSearch に移行するので、マーチャントはAdobe Commerce 2.4.4 以降にアップグレードする前に、Elasticsearchの代わりに OpenSearch を使用する必要があります。 Adobe Commerceのオンプレミスデプロイメントを使用するマーチャントは、Adobe Commerceが引き続き両方をサポートするので、Elasticsearchまたは OpenSearch を使用できます。


## OpenSearch とは

OpenSearch はElasticsearchと Kibana のフォークです。 Elastic.co の代わりにAWSが管理します。 詳しくは、GitHub を参照してください。 [opensearch-project/OpenSearch](https://github.com/opensearch-project/OpenSearch).

**バージョン間の互換性：**

**Adobe Commerce on cloud infrastructure はElasticsearch 7.10 をサポートしますか？**

**はい** - 2022 年 1 月中旬以降、クラウドインフラストラクチャバージョン 2.4.3-p1、2.4.3-p2、2.3.7-p3 でのAdobe Commerceは、Elasticsearch 7.10 をサポートします。

Adobe Commerceのオンプレミスの場合は、Log4j を軽減するために、最新バージョン 7.16.x をお勧めします。

## 移行：

## マーチャントはいつ OpenSearch に移行できますか？

Adobe Commerce 2.4.4 以降。

ただし、Adobe Commerce 2.4.4 へのアップグレードプロセスを開始する前に、マーチャントは、Elasticsearch 7.10 をサポートする最新バージョンのAdobe Commerceを使用しており、Adobe Commerce 2.4.4 または OpenSearch へのアップグレードプロセスを開始する前に、少なくともElasticsearchを使用している必要があります。

## 2.4.4 以外のマーチャント（Adobe Commerce on クラウドインフラストラクチャーおよびAdobe Commerce オンプレミス）では、何ができますか？ サポートされているElasticsearchバージョン（7.10、7.16.1）または OpenSearch にアップグレードできますか？ これを行うには、サポートされている最新バージョン（2.4.3-p1、2.3.7-p2、2.4.3-p1 など）である必要がありますか？

使用しているAdobe Commerce コアバージョンがElasticsearch 7.10 をサポートしている場合は、そのバージョンを使用できます。

レビュー [必要システム構成](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) バージョンの互換性については、開発者向けドキュメントを参照してください。

>[!NOTE]
>
>2022 年 5 月にElasticsearch 7.10 がサポート終了となるため、できるだけ早くAdobe Commerce 2.4.4 へのアップグレードを計画することをお勧めします。

Adobeパートナーは、ベータ版プログラムに新規登録できます [こちら](https://experienceleague.adobe.com/docs/commerce-operations/release/beta-program.html) Elasticsearch 7.16.1 および OpenSearch 1.1 に対してテストされた最新の beta4 コードにアクセスするには、
