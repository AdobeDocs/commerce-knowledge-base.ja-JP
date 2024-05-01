---
title: ElasticSuite トラッキングインデックスが原因でElasticsearchの問題が発生する
description: この記事では、ElasticSuite プラグインによって生成されるトラッキングインデックスによって引き起こされるElasticsearchメモリの問題の問題について説明します。
exl-id: 67bfd06a-c801-4306-8510-a84a6fe5351a
source-git-commit: c1c2bd29e14f4cbfffb235801e95ec7cbb7c7a55
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# ElasticSuite トラッキングインデックスが原因でElasticsearchの問題が発生する

>[!NOTE]
>
>ElasticSuite とその関連アプリケーションは、現在Adobeでサポートされていないサードパーティ製ツールです。 このコンテンツは情報提供のみを目的としており、サポート範囲に対して有効な内容を示すものではありません。

この記事では、ElasticSuite プラグインによって生成されるトラッキングインデックスによって引き起こされるElasticsearchメモリの問題の問題について説明します。

## 影響を受ける製品とバージョン

ElasticSuite 2.8.0 より前のバージョンでは、トラッキングインデックスを定期的にクリーンアップすることはできません。

2.9.8/2.10.7 より前のバージョンの ElasticSuite は、トラッキングインデックスを毎日のインデックスに保存しているので、オープンインデックスの数が増えます。

## 問題

ElasticSuite サードパーティプラグインがインストールされている場合、Elasticsearchメモリの問題が発生し、ElasticSuite トラッキングインデックスが原因でElasticsearchサービスがクラッシュする可能性があります。 症状は次のとおりです。

* メモリエラーが発生せずにElasticsearchがクラッシュする。
* health コマンドを実行する場合 `curl -m1 localhost:9200/_cluster/health?pretty` または `curl -m1 elasticsearch.internal:9200/_cluster/health?pretty` （スターターアカウントの場合）数は数百または数千です `unassigned_shards`
* Elasticsearchまたはサイトのパフォーマンスが著しく低下している。
* *「クラスターにアライブなノードが見つかりません」* Elasticsearchで deploy エラーまたは log エラーが発生しました。
* *「へのマッピングの更新を却下します [&lt;\*>_ tracking_log_event _&lt;\*>]“* デプロイまたはログのエラーで。

## 原因：

ElasticSuite には、トラッキングインデックスを作成する新機能があります。 これらのトラッキングインデックスでは、どの検索用語が最も使用されているか、どの用語が最も売上高を生み出しているか、どの用語が結果のないページにつながっているかを記録しているので、マーチャントは同義語を作成してそれらを修正できます。 トラッキングインデックスが削除されていないように見えるので、Elasticsearchがリソースを使い果たしてクラッシュします。

## 解決策

### トラッキングインデックスを定期的にクリーンアップできるように、ElasticSuite のバージョンをアップグレードしてください

ElasticSuite プラグインを 2.8.0 より上のバージョンにアップグレードしたら、インデックスの定期的なクリーニングを設定できます。

に移動 **ストア** > **設定** > **トラッキング** > **グローバル設定** > **リテンション遅延**

デフォルトの保持期間は 365 日です。 30 日または 15 日に減らすことができます。

### ElasticSuite のバージョンをアップグレードして、日単位のインデックスではなく月単位のインデックスを使用するようにします

ElasticSuite プラグインをバージョン > 2.9.8 / 2.10.7 にアップグレードすると、トラッキングインデックスは月単位になります。

引き続き、保持期間を短縮できます。

に移動 **ストア** > **設定** > **トラッキング** > **グローバル設定** > **リテンション遅延**

デフォルトの保持期間は 12 か月です（12 個のインデックスが生成されます）。 3 か月または 6 か月に減らすことができます。

### cronjob を使用してトラッキングインデックスデータをクリーンアップ

Cron ジョブを作成して、トラッキングインデックスを削除します。 このコマンドは、先月に作成したインデックスを削除します。

```
   curl -XDELETE localhost:9200/<name in index> * **\_tracking\_log** * _$(date
    +'%Y%m' -d 'last month')*
```

設定された時間頻度でインデックスを削除する場合は、開発者向けドキュメントの以下の記事を参照して、cron ジョブを作成します。

* [カスタム cron ジョブと cron グループの設定（チュートリアル）](https://devdocs.magento.com/guides/v2.3/config-guide/cron/custom-cron-tut.html)
* [cron ジョブの設定](https://devdocs.magento.com/guides/v2.3/cloud/configure/setup-cron-jobs.html)
