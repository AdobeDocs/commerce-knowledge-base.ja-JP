---
title: Elasticsearchインデックスのステータスが「イエロー」または「レッド」である
description: この記事では、Elasticsearchインデックスのステータスが「*green*」でない場合の解決策を提供します。 '*yellow*'は正常を示し、'*red*'は不良を示します。 「黄」または「赤」ステータスは、製品が見つからない場合や、古い製品情報が表示される場合に発生する可能性があります。
exl-id: 27689511-6a41-41a9-8dda-a627d2f65263
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Elasticsearchインデックスのステータスが「イエロー」または「レッド」である

>[!WARNING]
>
> [MySQL カタログ検索エンジンは、Adobe Commerce 2.4.0 で削除されます](/help/announcements/adobe-commerce-announcements/mysql-catalog-search-engine-will-be-removed-in-magento-2-4-0.md). バージョン 2.4.0 をインストールする前に、Elasticsearch・ホストをセットアップして構成する必要があります。こちらを参照してください [Elasticsearchのインストールと設定](https://devdocs.magento.com/guides/v2.3/config-guide/elasticsearch/es-overview.html).

この記事では、Elasticsearchインデックスのステータスが「」でない場合の修正点を説明します&#x200B;*緑*&#39;. &#39;*黄*&#39;は標準を示し、&#39;*赤*&#39;は無効を示します。 「黄」または「赤」ステータスは、製品が見つからない場合や、古い製品情報が表示される場合に発生する可能性があります。

## 影響を受けるバージョンと製品

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x
* Adobe Commerce オンプレミス 2.2.x、2.3.x

## 問題

Elasticsearchカタログ検索インデックスが遅いため、「」のステータスになります&#x200B;*黄*&#39;または&#39;*赤*「」ではなく「」*緑*&#39;. また、フロントエンドで変更が見つからない可能性もあります。

## 原因：

考えられる原因はいくつかあります。 原因の 1 つは、Elasticsearchインスタンスのディスク容量が不足していることです。 もう 1 つの原因は、インデックスの重複です。

## 解決策

これらの手順を実行する前に新しい mysql ダンプを作成し、営業時間外に実行して、クライアントに影響を与える可能性を回避します。

1. 一時的に MySQL 検索に切り替える – MySQL 検索を有効にします。 （メモ：必ずElasticsearchに戻してください。戻すと、パフォーマンスの問題が発生する場合があります）。
1. 重複したインデックスを識別するには、次のコマンドを実行します。

   ```
   curl --silent -X GET localhost:9200/_cat/indices?v
   ```

1. インデックスを削除するには：

   ```
   curl -XDELETE localhost:9200/[your_index_name_here]
   ```

1. Elasticsearchを再度有効にします。
1. 完全な再インデックスを実行します。
1. 次のコマンドを実行して、インデックスのステータスを確認します。

   ```
   curl --silent -X GET localhost:9200/_cat/indices?v
   ```

これらの手順が機能しない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

## 関連資料

詳しくは、次を参照してください [Elasticsearchクラスターヘルス API](https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-health.html).
