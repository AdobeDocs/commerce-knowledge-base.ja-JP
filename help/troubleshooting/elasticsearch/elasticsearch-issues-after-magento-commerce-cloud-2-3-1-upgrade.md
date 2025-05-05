---
title: Adobe Commerce cloud infrastructure 2.3.1 以降のアップグレード後のElasticsearchの問題
description: この記事では、Elasticsearchバージョン 2.x および 5.x を使用している場合に、クラウドインフラストラクチャバージョン 2.3.1 以降のAdobe Commerceにアップグレードした後のデプロイメント中に発生する問題の解決策について説明します。
exl-id: 6ceeb2ea-528d-4c03-ab2b-c5aed46fd0a2
feature: Cloud
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Adobe Commerce cloud infrastructure 2.3.1 以降のアップグレード後のElasticsearchの問題

>[!WARNING]
>
>[MySQL カタログ検索エンジンは、Adobe Commerce 2.4.0 で削除されます ](/help/announcements/adobe-commerce-announcements/mysql-catalog-search-engine-will-be-removed-in-magento-2-4-0.md)。 バージョン 2.4.0 をインストールする前に、Elasticsearch・ホストをセットアップして構成する必要があります。[Elasticsearchのインストールと設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) を参照してください。

>[!WARNING]
>
>なお、実稼働環境へのサービスのアップグレードは、インフラストラクチャチームへの 48 営業時間以内通知を行わなければ実行できません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)48 時間前に、必要なサービスアップグレードの詳細と、アップグレードプロセスを開始する時刻を指定します。

この記事では、Elasticsearchバージョン 2.x および 5.x を使用している場合に、クラウドインフラストラクチャバージョン 2.3.1 以降のAdobe Commerceにアップグレードした後のデプロイメント中に発生する問題の解決策について説明します。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー 2.3.1 以降のAdobe Commerce
* Elasticsearch 2.x および 5.x

## 原因：

クラウドインフラストラクチャー上でAdobe Commerceにアップグレードし（バージョン 2.3.1 以降）、バージョン 6.x より前のElasticsearchを使用しているマーチャントでは、デプロイ時にエラーが発生する場合があります。 これは、Elasticsearchバージョン 2.x と 5.x が [ 提供終了 ](https://www.elastic.co/support/eol) であり、Adobe Commerceではサポートされなくなったためです。 Elasticsearchクライアントは最新である必要があります。最新でない場合、デプロイメントを実行するとエラーが発生するリスクがあります。 詳しくは、開発者向けドキュメントの [Elasticsearchクライアントの変更 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) を参照してください。

## 問題

デプロイすると、Elasticsearchバージョンに互換性がないことを示す、次のようなエラーメッセージが表示されます。*インフラストラクチャレイヤーのElasticsearchサービスバージョン 5.2.2 は、Magentoアプリケーションで使用される現在のバージョンの elasticsearch/elasticsearch module （6.7.0.0）と互換性がありません。* *この問題を解決するには、Magentoのクラウドインフラストラクチャ上のElasticsearchサービスをバージョン 6.x にアップグレードします*。 この問題の他の症状は、画像が欠落していたり、環境のフィルターに関する問題が発生していたりする場合があります。

## 解決策

>[!WARNING]
>
>共有環境がある場合は、ステージング環境と実稼動環境がアップグレードする準備ができていることを確認します。

この問題を解決するには、ElasticsearchクライアントモジュールとElasticsearchサービスが、最新の推奨バージョンである必要があります。

1. 開発者向けドキュメントの手順 [Elasticsearchモジュールの変更 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) に従って、Elasticsearchクライアントモジュールの最新のお勧めバージョンを入手します。
1. [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) し、ステージング環境と実稼動環境で、Elasticsearchサービスを 6.x にアップデートするようにリクエストします。 Elasticsearchサービスへのアップグレードが完了するまでに時間がかかる場合があることに注意してください。

## 関連資料

* [Adobe Commerce 2.3 テクノロジースタック要件 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/overview) については、開発者向けドキュメントを参照してください。
* 開発者向けドキュメントの [Elasticsearchサービスを設定する ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/service/elasticsearch) を参照してください。
* 開発者向けドキュメントの [Elasticsearchのインストールと設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) を参照してください。
* [Elasticsearchが正しくインストールされていることを確認する ](/help/troubleshooting/elasticsearch/ensure-elasticsearch-is-installed-properly.md) については、サポートナレッジベースを参照してください。
