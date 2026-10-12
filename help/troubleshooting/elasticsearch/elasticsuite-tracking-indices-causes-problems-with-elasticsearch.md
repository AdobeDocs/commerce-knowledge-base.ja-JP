---
title: ElasticSuite トラッキングインデックスがElasticsearchの問題を引き起こす
description: この記事では、ElasticSuite プラグインによって生成されたインデックスのトラッキングによって発生するElasticsearch メモリの問題について説明します。
exl-id: 67bfd06a-c801-4306-8510-a84a6fe5351a
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%
---
# ElasticSuite トラッキングインデックスがElasticsearchの問題を引き起こす

>[!NOTE]
>
>ElasticSuiteとその関連アプリケーションは、現在Adobeでサポートされていないサードパーティツールです。 このコンテンツは情報提供のみとして表示され、サポート対象として有効な内容を示すものではありません。

この記事では、ElasticSuite プラグインによって生成されたインデックスのトラッキングによって発生するElasticsearch メモリの問題について説明します。

## 影響を受ける製品とバージョン

2.8.0より前のバージョンのElasticSuiteでは、トラッキングインデックスを定期的にクリーンアップできません。

ElasticSuite バージョン 2.9.8 / 2.10.7より前のバージョンでは、トラッキングインデックスを毎日のインデックスに保存しているため、開いているインデックスの数が増加します。

## イシュー

ElasticSuite サードパーティ製プラグインがインストールされている場合、Elasticsearch メモリの問題が発生し、ElasticSuite トラッキングインデックスによってElasticsearch サービスがクラッシュする可能性があります。 症状は次のとおりです。

* Elasticsearchがクラッシュし、メモリエラーが発生しません。
* ヘルスコマンド `curl -m1 localhost:9200/_cluster/health?pretty`または`curl -m1 elasticsearch.internal:9200/_cluster/health?pretty` （スターターアカウントの場合）を実行すると、数百または数千の`unassigned_shards`が存在します
* Elasticsearchまたはサイトのパフォーマンスが大幅に低下する。
* *「クラスターにアライブノードが見つかりません」* （Elasticsearchのデプロイまたはログエラー）。
* デプロイまたはログエラーの&#x200B;*「マッピングの更新を[&lt;\*>_tracking_ log_event_&lt;\*>]&quot;*に拒否しています。

## 原因

ElasticSuiteには、トラッキングインデックスを作成する新機能があります。 これらのトラッキングインデックスは、最も頻繁に使用されている検索語、最も回転率が高い用語、どの用語が「検索結果なし」のページにつながっているかを記録し、加盟店が類義語を作成して修正できるようにします。 トラッキングインデックスは削除されないようなので、Elasticsearchのリソースが不足してクラッシュします。

## Solution

### トラッキングインデックスを定期的にクリーンアップできるように、ElasticSuite バージョンをアップグレードします

ElasticSuite プラグインを2.8.0より高いバージョンにアップグレードすると、インデックスの定期的なクリーニングを設定できます。

**ストア** > **設定** > **トラッキング** > **グローバル設定** > **保持遅延**&#x200B;に移動します

デフォルトの保持期間は365日です。 30日や15日に短縮することもできます。

### ElasticSuiteのバージョンをアップグレードして、日次ベースのインデックスではなく月次ベースのインデックスを使用します

ElasticSuite プラグインをバージョン > 2.9.8 / 2.10.7にアップグレードすると、トラッキングインデックスは月次ベースになります。

リテンション期間を短縮することもできます。

**ストア** > **設定** > **トラッキング** > **グローバル設定** > **保持遅延**&#x200B;に移動します

デフォルトの保持期間は12か月です（12のインデックスが生成されます）。 3か月か6か月に短縮できます。

### トラッキングインデックスデータのクリーンアップにcronjobを使用する

トラッキングインデックスを削除するcron ジョブを作成します。 このコマンドは、先月作成されたインデックスを削除します。

```
   curl -XDELETE localhost:9200/<name in index> * **\_tracking\_log** * _$(date
    +'%Y%m' -d 'last month')*
```

特定の時間頻度でインデックスを削除する場合は、開発者ドキュメントの次の記事を参照して、cron ジョブを作成します。

* [カスタム cron ジョブとcron グループの設定（チュートリアル）](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/crons/custom-cron-tutorial)
* [cron ジョブの設定](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property)
