---
title: MySQL とElasticsearchで異なる結果が表示される
description: この記事では、MySQL とElasticsearchで同じ検索クエリに対して異なる検索結果を取得することに関連する、Adobe Commerce on cloud infrastructure 2.2.3 の既知の問題に対するパッチを提供します。
exl-id: 37a0164a-0237-4200-ab9c-e0dbad7e2062
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# MySQL とElasticsearchで異なる結果が表示される

>[!WARNING]
>
> [MySQL カタログ検索エンジンは、Adobe Commerce 2.4.0 で削除されます](/help/announcements/adobe-commerce-announcements/mysql-catalog-search-engine-will-be-removed-in-magento-2-4-0.md). バージョン 2.4.0 をインストールする前に、Elasticsearch・ホストをセットアップおよび構成する必要があります。こちらを参照してください [Elasticsearchのインストールと設定](https://devdocs.magento.com/guides/v2.3/config-guide/elasticsearch/es-overview.html) 開発者向けドキュメントを参照してください。

この記事では、MySQL とElasticsearchで同じ検索クエリに対して異なる検索結果を取得することに関連する、Adobe Commerce on cloud infrastructure 2.2.3 の既知の問題に対するパッチを提供します。

## 問題：

同じフィルターセットを使用したカタログ検索結果は、使用する検索エンジン（MySQL またはElasticsearch）によって異なります。

<u>再現手順</u> :

1. Elasticsearchをインストールして設定します。
1. ストアフロントで、フィルターのいずれかを選択します。
1. 一致する製品の数をメモします。
1. デフォルトの設定 [MySQL search](/help/announcements/adobe-commerce-announcements/mysql-catalog-search-engine-will-be-removed-in-magento-2-4-0.md).
1. ストアフロントで、フィルターのいずれかを選択します。
1. 一致する製品の数をメモします。

<u>期待される結果</u>：一致する製品の数は同じです。

<u>実際の結果</u>：一致する製品の数が異なります。

## パッチ

パッチはこの記事に添付されています。 パッチをダウンロードするには、記事の最後までスクロールして必要なファイル名をクリックするか、次のリンクをクリックします。

[MDVA-12312\_EE\_2.2.3\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-12312_EE_2.2.3_COMPOSER_v1.patch.zip)

[MDVA-14172\_EE\_2.2.6\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-14172_EE_2.2.6_COMPOSER_v1.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次の場合に作成されました。

* クラウドインフラストラクチャー 2.2.3 上のAdobe Commerce（ `MDVA-12312_EE_2.2.3_COMPOSER_v1.patch` ファイル）
* クラウドインフラストラクチャー 2.2.6 上のAdobe Commerce（ `MDVA-14172_EE_2.2.6_COMPOSER_v1.patch` ファイル）

この `MDVA-12312_EE_2.2.3_COMPOSER_v1.patch` patch は、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決する可能性があります）。

* クラウドインフラストラクチャー 2.2.4 上のAdobe Commerce
* クラウドインフラストラクチャー 2.2.5 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.2.3
* Adobe Commerce オンプレミス 2.2.4
* Adobe Commerce オンプレミス 2.2.5

この `MDVA-14172_EE_2.2.6_COMPOSER_v1.patch` patch は、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決する可能性があります）。

* Adobe Commerce オンプレミス 2.2.6

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 手順については、サポートナレッジベースを参照してください。

## 添付ファイル
