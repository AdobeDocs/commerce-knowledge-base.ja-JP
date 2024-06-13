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
>クラウドインフラストラクチャー上のAdobe Commerceの場合、インフラストラクチャチームに 48 営業時間前に通知しない限り、実稼動環境にサービスアップグレードをプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要があるのは、48 時間前までということになります [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) 必要なサービスのアップグレードの詳細を説明し、アップグレードプロセスを開始する時刻を指定します。

## 手順 1 - Elasticsearchの問題を確認 {#step-1}

+++**あなたの問題はElasticsearchに関係があるのでしょうか？**

エラーメッセージに示されるElasticsearchの問題「_クラスターにアライブ ノードが見つかりません」、_ 製品が見つからない、および古い製品情報が表示される。

a.はい – に進みます。 [手順 2](#step-2).\
b.いいえ – で関連する検索語句を再度検索します。 [Adobe Commerce ヘルプセンターのナレッジベース](https://support.magento.com/hc).

+++

## 手順 2 - インストールの問題を確認 {#step-2}

+++**Elasticsearchの新しいインストールですか？**

a.はい –  [Elasticsearchが正しく取り付けられていることを確認します。](/help/troubleshooting/elasticsearch/ensure-elasticsearch-is-installed-properly.md) また、クラウドインフラストラクチャー 2.3.1 以降でAdobe Commerceを使用しているかどうかも確認します。 クラウドインフラストラクチャー上でAdobe Commerceにアップグレードし（バージョン 2.3.1 以降）、バージョン 6.x より前のElasticsearchを使用しているマーチャントでは、デプロイ時にエラーが発生する場合があります。 この問題を解決するには、ElasticsearchクライアントモジュールとElasticsearchサービスを最新の推奨バージョンにする必要があります。 手順については、を参照してください。 [Adobe Commerce on cloud infrastructure 2.3.1 以降へのアップグレード後のElasticsearchの問題](/help/troubleshooting/elasticsearch/elasticsearch-issues-after-magento-commerce-cloud-2-3-1-upgrade.md).\
b.いいえ – クラスターの正常性を確認してください。 ステージング環境または実稼動環境で作業している場合は、次のコマンドを実行します。 `curl -m1 localhost:9200/_cluster/health?pretty`. （すべてのスターター分岐を含む）統合環境で実行している場合 `curl -m1 elasticsearch.internal:9200/_cluster/health?pretty`. 次の手順に進みます。 [手順 3](#step-3).

+++

## 手順 3 - Elasticsearchクラスターが使用可能かどうかを確認する {#step-3}

+++**サービスの応答を受け取りましたか？**

a.はい – に進みます。 [手順 4](#step-4).\
b.いいえ – に進みます。 [手順 9](#step-9).

+++

## 手順 4 - Elasticsearchクラスターが正常であることを確認する {#step-4}

+++**グリーンに応答？**

a.はい。Elasticsearchはデータの処理に使用でき、インデックス再作成は機能します。 次の手順に進みます。 [手順 5](#step-5).\
b. NO – 黄または赤は、ノード間の接続に問題があり、一部のデータが使用できないことを意味します。 黄色の場合は、次のコマンドを実行します。 `php bin/magento config:show catalog/search/engine` をクリックして、検索エンジンを確認します。 次の手順に進みます。 [手順 6](#step-6). 赤の場合、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 5 – 検索の動作の確認 {#step-5}

+++**検索の問題？**

現象には、製品がない、空のカテゴリが含まれている、製品または製品カテゴリが正しくない更新が含まれていない、などがあります。

a.はい – このコマンドを実行して、カタログ検索のステータスをチェックします。 `php bin/magento indexer:status`. 次の手順に進みます。 [手順 8](#step-8).\
b. NO - コマンドを実行します。 `php bin/magento config:show catalog/search/engine`. 次の手順に進みます。 [手順 6](#step-6).

+++

## 手順 6 - ElasticSuite を確認 {#step-6}

+++**ElasticSuite は使用中ですか？**

a.はい – 次のコマンドを実行して、ElasticSuite が現在のバージョンであるかどうかを確認します。 `cat composer.lock | grep -A 1 elasticsuite | grep '"version"'` このバージョンが非推奨（廃止予定）になっているか推奨されているかを確認するには、を参照してください。 [Github: Smile-SA/elasticsuite](https://github.com/Smile-SA/elasticsuite). ElasticSuite が最新の場合は、次に進みます。 [手順 10](#step-10).\
b.いいえ – に進みます。 [手順 7](#step-7).

+++

## 手順 7 - ECE ツールの最新情報を確認 {#step-7}

+++**ECE-tools は最新バージョンですか？**

次のコマンドを実行します。 `php ./vendor/bin/ece-tools -V` そして、ECE-tools のバージョンを確認します。 これは [ece-tools の最新バージョン](https://github.com/magento/ece-tools/releases)?

a.はい – に進みます。 [ステップ 5a](#step-5).\
b.いいえ – ECE-tools を最新バージョンにアップグレードします。 コマンドを実行します `php bin/magento config: show catalog/search/engine` をクリックして、検索エンジンを確認します。 次の手順に進みます。 [手順 6](#step-6).

+++

## 手順 8 – 再インデックス化の確認 {#step-8}

+++**でのカタログ検索ステータス _処理_?**

a.はい – 処理が完了するまで待ってから、製品カテゴリが更新されたかどうかを確認する必要があります。 まだ設定されていない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).\
b. NO - カタログ検索のステータスが _再インデックスが必要です_ cli/ターミナルで実行します。 `php bin/magento cron:run`. これが機能しない場合は、次を実行します。 `php bin/magento indexer:reindex`. それでも問題が解決しない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 9 - yaml 設定の確認 {#step-9}

+++**`.yaml`ファイルが最近更新されたとき**

a.はい – 確認 `.yaml` DevDocs を参照したElasticsearch設定 [Elasticsearchの設定：Elasticsearchを有効にします。](https://devdocs.magento.com/cloud/project/project-conf-files_services-elastic.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=elastic%20search%20yaml).\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

## 手順 10 - トラッキングインデックスを確認 {#step-10}

+++**トラッキングインデックスはリストされていますか。**

実行 `curl elasticsearch.internal:9200/_cat/indices` （すべてのスターターブランチを含む統合環境を使用している場合）。 ステージング環境または実稼動環境で実行している場合は、次のコマンドを実行します `curl localhost:9200/_cat/indices`. トラッキングインデックスはリストされていますか。 の出力を確認します`_tracking_log_`.

a.はい – バージョン 2.8.0 より前の ElasticSuite を使用している場合は、以下を実行することをお勧めします。 [elasticSuite 2.8.0 へのアップグレードによるトラッキングインデックスの保持の調整またはトラッキングの無効化](https://support.magento.com/hc/en-us/articles/360035266131?). すぐにアップグレードできない場合は、次のことができます [cron を作成してトラッキングインデックスを削除](/help/troubleshooting/elasticsearch/elasticsuite-tracking-indices-causes-problems-with-elasticsearch.md). ただし、パフォーマンスの問題が発生する可能性があります。 ElasticSuite 2.8.0 にアップグレードするか、トラッキングインデックスを削除したら、コマンドを実行します（Pro ステージング環境または実稼動環境の場合）。`localhost:9200/_cat/allocation?v` 空き領域を確認します。 いずれかの統合環境（すべてのスターターブランチを含む）で実行している場合は、次の操作を実行します `elasticsearch.internal:9200/_cat/allocation?v`. 次の手順に進みます。 [手順 11](#step-11).\
b.いいえ – ステージング環境または実稼動環境で実行している場合 `localhost:9200/_cat/allocation?v` 空き容量を確認します。 いずれかの統合環境（すべてのスターターブランチを含む）で実行している場合は、次の操作を実行します `elasticsearch.internal:9200/_cat/allocation?v`. 次の手順に進みます。 [手順 11](#step-11).

+++

## 手順 11 – 特定のエラーの検索 {#step-11}

+++**具体的なエラーは？**

Adobe Commerceと ES のログ、拡張機能およびカスタムコード。

a.はい – Adobe Commerce ヘルプセンターのトラブルシューティング記事を確認してください [Elasticsearchが正しくインストールされていることを確認します。](/help/troubleshooting/elasticsearch/ensure-elasticsearch-is-installed-properly.md) または [ElasticSuite プラグインを使用すると、Elasticsearchがクラッシュするか、メモリ不足の問題が発生する](https://support.magento.com/hc/en-us/articles/360035266131).\
b.いいえ – に進みます。 [手順 12](#step-12).

+++

## 手順 12 – 使用可能なストレージを確認する {#step-12}

+++**ストレージ使用率 > 85%?**

a.はい。利用可能なストレージを増やす必要があります。 DevDocs を参照してください[Elasticsearchの設定：Elasticsearchを有効にします。](https://devdocs.magento.com/cloud/project/project-conf-files_services-elastic.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=elastic%20search%20yaml). 次を実行します。 `localhost:9200/_cat/allocation?v` （Pro ステージング環境または実稼動環境の場合）。 いずれかの統合環境（すべてのスターターブランチを含む）で実行している場合は、次のコマンドを実行します。 `elasticsearch.internal:9200/_cat/allocation?v`. 次の手順に進みます。 [手順 11](#step-11).\
b.いいえ –  [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

+++

[手順 1 に戻る](#step-1)
