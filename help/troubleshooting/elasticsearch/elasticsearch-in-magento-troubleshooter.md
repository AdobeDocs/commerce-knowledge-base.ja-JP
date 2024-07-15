---
title: Adobe CommerceのElasticsearchに関するトラブルシューティング
description: Adobe CommerceのElasticsearchに関する問題は、Elasticsearchのトラブルシューティング ツールを使用して解決できます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。
exl-id: acae0da0-2918-4021-9fbe-c138940c5a72
feature: Categories
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Adobe CommerceのElasticsearchに関するトラブルシューティング

Adobe CommerceのElasticsearchに関する問題は、Elasticsearchのトラブルシューティング ツールを使用して解決できます。 各質問をクリックすると、トラブルシューティングの各ステップの回答が表示されます。

>[!WARNING]
>
>クラウドインフラストラクチャー上のAdobe Commerceの場合、インフラストラクチャチームに 48 営業時間前に通知しない限り、実稼動環境にサービスアップグレードをプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)48 時間前に、必要なサービスアップグレードの詳細と、アップグレードプロセスを開始する時刻を指定します。

## 手順 1 - Elasticsearchの問題を確認 {#step-1}

+++**あなたの問題はElasticsearchに関連していますか？**

Elasticsearchの問題は、エラーメッセージ、「_クラスターに No alive node found in your cluster」、製品の欠落_ および古い製品情報の表示で示されます。

a.はい – [ 手順 2](#step-2) に進みます。\
b.いいえ。関連する検索用語について、[Adobe Commerce ヘルプセンターのナレッジベース ](https://support.magento.com/hc) で再度検索してください。

+++

## 手順 2 - インストールの問題を確認 {#step-2}

+++**Elasticsearchの新規インストールですか？**

a.はい – [Elasticsearchが正しくインストールされていることを確認します。](/help/troubleshooting/elasticsearch/ensure-elasticsearch-is-installed-properly.md) また、Cloud Infrastructure 2.3.1 以降でAdobe Commerceを使用しているかどうかも確認してください。 クラウドインフラストラクチャー上でAdobe Commerceにアップグレードし（バージョン 2.3.1 以降）、バージョン 6.x より前のElasticsearchを使用しているマーチャントでは、デプロイ時にエラーが発生する場合があります。 この問題を解決するには、ElasticsearchクライアントモジュールとElasticsearchサービスを最新の推奨バージョンにする必要があります。 手順については、[Adobe Commerce on cloud infrastructure 2.3.1 以降のアップグレード後のElasticsearchの問題 ](/help/troubleshooting/elasticsearch/elasticsearch-issues-after-magento-commerce-cloud-2-3-1-upgrade.md) を参照してください。\
b.いいえ – クラスターの正常性を確認してください。 Pro ステージング環境または実稼動環境にいる場合は、次のコマンドを実行します：`curl -m1 localhost:9200/_cluster/health?pretty`。 （すべてのスターター分岐を含む）統合環境で作業している場合は、`curl -m1 elasticsearch.internal:9200/_cluster/health?pretty` を実行します。 [ 手順 3](#step-3) に進みます。

+++

## 手順 3 - Elasticsearchクラスターが使用可能かどうかを確認する {#step-3}

+++**サービス応答を受け取りましたか？**

a.はい – [ 手順 4](#step-4) に進みます。\
b.いいえ – [ 手順 9](#step-9) に進みます。

+++

## 手順 4 - Elasticsearchクラスターが正常であることを確認する {#step-4}

+++**応答が緑？**

a.はい。Elasticsearchはデータの処理に使用でき、インデックス再作成は機能します。 [ 手順 5](#step-5) に進みます。\
b. NO – 黄または赤は、ノード間の接続に問題があり、一部のデータが使用できないことを意味します。 黄色の場合は、`php bin/magento config:show catalog/search/engine` コマンドを実行して、検索エンジンを確認します。 [ 手順 6](#step-6) に進みます。 赤い場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。

+++

## 手順 5 – 検索の動作の確認 {#step-5}

+++**検索の問題？**

現象には、製品がない、空のカテゴリが含まれている、製品または製品カテゴリが正しくない更新が含まれていない、などがあります。

a.はい – このコマンドを実行して、カタログ検索のステータスをチェックします。`php bin/magento indexer:status` [ 手順 8](#step-8) に進みます。\
b. NO - コマンド `php bin/magento config:show catalog/search/engine` を実行します。 [ 手順 6](#step-6) に進みます。

+++

## 手順 6 - ElasticSuite を確認 {#step-6}

+++**ElasticSuite が使用中ですか？**

a.はい – 次のコマンドを実行して、ElasticSuite が現在のバージョンかどうかを確認します。`cat composer.lock | grep -A 1 elasticsuite | grep '"version"'` このバージョンが非推奨（廃止予定）になっているか、推奨されているかを確認するには、[Github:Smile-SA/elasticsuite](https://github.com/Smile-SA/elasticsuite) を参照してください。 ElasticSuite が最新の場合は [ 手順 10](#step-10) に進みます。\
b.いいえ – [ 手順 7](#step-7) に進みます。

+++

## 手順 7 - ECE ツールの最新情報を確認 {#step-7}

+++**ECE-tools は最新バージョンですか？**

`php ./vendor/bin/ece-tools -V` コマンドを実行して、ECE-tools のバージョンを確認します。 [ECE ツールの最新版 ](https://github.com/magento/ece-tools/releases) ですか？

a.はい – [ ステップ 5a](#step-5) に進みます。\
b.いいえ – ECE-tools を最新バージョンにアップグレードします。 コマンド `php bin/magento config: show catalog/search/engine` を実行して、検索エンジンを確認します。 [ 手順 6](#step-6) に進みます。

+++

## 手順 8 – 再インデックス化の確認 {#step-8}

+++**カタログ検索のステータスは _処理中_ ですか？**

a.はい – 処理が完了するまで待ってから、製品カテゴリが更新されたかどうかを確認する必要があります。 まだ承認されていない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。\
b. NO - カタログ検索のステータスが _再インデックスが必要_ の場合は、CLI/ターミナルで実行します：`php bin/magento cron:run`。 これが機能しない場合は、`php bin/magento indexer:reindex` を実行します。 それでも問題が解決しない場合は、[ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。

+++

## 手順 9 - yaml 設定の確認 {#step-9}

+++ファイル **`.yaml`最近更新されましたか？**

a.はい – DevDocs`.yaml` 参照してElasticsearch設定を確認します [ 設定をElasticsearchするには、Elasticsearch：を設定します ](https://devdocs.magento.com/cloud/project/project-conf-files_services-elastic.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=elastic%20search%20yaml)。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

## 手順 10 - トラッキングインデックスを確認 {#step-10}

+++**トラッキングインデックスはリストされていますか？**

`curl elasticsearch.internal:9200/_cat/indices` を実行します（すべてのスターター分岐を含む統合環境を使用している場合）。 Pro ステージング環境または実稼動環境の場合は、`curl localhost:9200/_cat/indices` を実行します。 トラッキングインデックスはリストされていますか。 出力で `_tracking_log_` をチェックします。

a.はい。バージョン 2.8.0 より前の ElasticSuite を使用している場合は、[ElasticSuite 2.8.0 にアップグレードしてトラッキングインデックスの保持を調整するか、トラッキングを無効にする ](https://support.magento.com/hc/en-us/articles/360035266131?) ことをお勧めします。 すぐにアップグレードできない場合は、[cron を作成してトラッキングインデックスを削除 ](/help/troubleshooting/elasticsearch/elasticsuite-tracking-indices-causes-problems-with-elasticsearch.md) できます。 ただし、パフォーマンスの問題が発生する可能性があります。 ElasticSuite 2.8.0 にアップグレードするか、トラッキングインデックスを削除したら、（Pro ステージング環境または実稼動環境の場合は）:`localhost:9200/_cat/allocation?v` コマンドを実行し、利用可能な領域を確認します。 いずれかの統合環境（すべてのスターターブランチを含む）で作業している場合は、`elasticsearch.internal:9200/_cat/allocation?v` を実行します。 [ 手順 11](#step-11) に進みます。\
b. NO - Pro ステージング環境または実稼動環境で実行している場合は、`localhost:9200/_cat/allocation?v` を実行し、使用可能な領域を確認します。 いずれかの統合環境（すべてのスターターブランチを含む）で作業している場合は、`elasticsearch.internal:9200/_cat/allocation?v` を実行します。 [ 手順 11](#step-11) に進みます。

+++

## 手順 11 – 特定のエラーの検索 {#step-11}

+++**特定のエラー？**

Adobe Commerceと ES のログ、拡張機能およびカスタムコード。

回答：はい。Adobe Commerce ヘルプセンターのトラブルシューティング記事 [Elasticsearchが正しくインストールされていることを確認してください ](/help/troubleshooting/elasticsearch/ensure-elasticsearch-is-installed-properly.md)、または [ElasticSuite プラグインを使用する際に、Elasticsearchがクラッシュするか、メモリ不足の問題が発生します ](https://support.magento.com/hc/en-us/articles/360035266131)。\
b.いいえ – [ 手順 12](#step-12) に進みます。

+++

## 手順 12 – 使用可能なストレージを確認する {#step-12}

+++**ストレージ使用率 > 85%?**

a.はい。利用可能なストレージを増やす必要があります。 DevDocs[ 設定Elasticsearch:Elasticsearchを有効にするには、を参照してください ](https://devdocs.magento.com/cloud/project/project-conf-files_services-elastic.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=elastic%20search%20yaml) 次に、`localhost:9200/_cat/allocation?v` を実行します（Pro ステージング環境または実稼動環境の場合）。 （すべてのスターターのブランチを含む）統合環境の 1 つにいる場合は、`elasticsearch.internal:9200/_cat/allocation?v` を実行します。 [ 手順 11](#step-11) に進みます。\
b.いいえ – [ サポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)。

+++

[手順 1 に戻る](#step-1)
