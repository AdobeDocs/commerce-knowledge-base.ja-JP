---
title: Elasticsearchサービスが実行されていません
description: この記事では、Elasticsearch（ES）サービスが実行されていない（通常はクラッシュの結果として発生する）場合に発生する可能性のあるエラーの解決策を示します。 症状としては、curl を使用したヘルスチェック実行時のエラー、コマンドラインを使用したインデックス再作成、Exception エラーと PHP エラー、製品ページでのエラーなどがあります。 この表は、エラーの一覧と、解決を試みるリソースへのリンクを示しています。 1 つの症状が様々な原因によって引き起こされる可能性があります。
exl-id: 2c2230de-cb30-4a03-8c3e-d9f44783dbae
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Elasticsearchサービスが実行されていません

この記事では、Elasticsearch（ES）サービスが実行されていない（通常はクラッシュの結果として発生する）場合に発生する可能性のあるエラーの解決策を示します。 症状としては、curl を使用したヘルスチェック実行時のエラー、コマンドラインを使用したインデックス再作成、Exception エラーと PHP エラー、製品ページでのエラーなどがあります。 この表は、エラーの一覧と、解決を試みるリソースへのリンクを示しています。 1 つの症状が様々な原因によって引き起こされる可能性があります。

## ElasticsearchバージョンとAdobe Commerceとの互換性

* Adobe CommerceのオンプレミスおよびAdobe Commerceのクラウドインフラストラクチャ：

   * v2.2.3 以降は、ES 5.x をサポート
   * v2.2.8+および v2.3.1+は、ES 6.x をサポートしています。
   * ES v2.x および v5.x は、[&#x200B; 提供終了 &#x200B;](https://www.elastic.co/support/eol) が理由で推奨されていません。 ただし、Adobe Commerce v2.3.1 を使用していて、ES 2.x または ES 5.x を使用する場合は、[Elasticsearch php クライアントを変更する &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) 必要があります。

* Magento Open Source v2.3.0 以降では、ES 5.x および 6.x がサポートされています（ただし 6.x をお勧めします）。

<table>
<tr>
<th>ES サービスが実行されていない場合の症状</th>
<th>詳細</th>
<th>リソース</th>
</tr>
<tr>
<td rowspan="3">例外エラー</td>
</tr>
<tr>
<td>
<code>&lbrace;"0":"&lbrace;\"error\":&lbrace;\"root_cause\":[{\"type\":\"illegal_argument_exception\",\"reason\":\"Fielddata is disabled on text fields by default. Set fielddata=true on [%attribute_code%]] in order to load fielddata in memory by uninverting the inverted index. Note that this can however use significant memory.\"}&rbrack;</code>
</td>
<td>
<a href="https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-5-is-configured-but-search-page-does-not-load-with-fielddata-is-disabled...-error.html?lang=ja">Elasticsearch 5 が設定されましたが、サポートナレッジベースに「Fielddata is disabled...」エラーが表示され </a> 検索ページが読み込まれません。
</td>
</tr>
<tr>
<td>
<code>Elasticsearch\Common\Exceptions\NoNodesAvailableException: Noticed exception 'Elasticsearch\Common\Exceptions\NoNodesAvailableException' with message 'No alive nodes found in your cluster' in /app/&lt;projectid&gt;/vendor/elasticsearch/elasticsearch/src/Elasticsearch/ConnectionPool/StaticNoPingConnectionPool.php:51</code>
</td>
<td>
Elasticsuite インデックスが削除されていません。  サポートナレッジベースの <a href="https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsuite-tracking-indices-causes-problems-with-elasticsearch.html?lang=ja">ElasticSuite トラッキングインデックスが原因でElasticsearchに関する問題が発生する </a> を参照してください。
 </td>
</tr>
<tr>
<td>PHP エラー</td>
<td>
<i> クラスター内にアクティブなノードが見つかりません","1":"#0 /app/&lt;projectid&gt;/vendor/elasticsearch/elasticsearch/src/Elasticsearch/Transport.php</i>
</td>
<td rowspan="4">
<ul>
<li>ディスク領域が不足しているリソース：<ul>
<li><a href="https://www.cyberciti.biz/datacenter/linux-unix-bsd-osx-cannot-write-to-hard-disk/">Linux および Unix システムのハードディスクの問題（ディスク容量超過やディスクへの書き込み不可など）を解決するための 8 つのヒント</a></li>
<li><a href="https://serverfault.com/questions/315181/df-says-disk-is-full-but-it-is-not">serverfault: df はディスクがいっぱいと言うが、ディスクが空ではない</a></li>
<li><a href="https://unix.stackexchange.com/questions/125429/tracking-down-where-disk-space-has-gone-on-linux">unix.stackexchange.com:Linux のディスク容量がどこにあるかを調べますか？</a></li>
<li>ログファイルは、定期的に十分にアーカイブされていません。 開発者向けドキュメントの <a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/action-logs/action-log-archive"> ログアーカイブの設定 </a> を参照してください。</li>
<li>ファイルシステムディレクトリは最適化されません。 開発者向けドキュメントの <a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/developer-tools#resource-file-optimization"> ファイルの最適化 </a> を参照してください。</li>
<li>上記のドキュメントの解決策でも問題が解決しない場合は、Adobeアカウントチームに連絡して追加のストレージをリクエストすることを検討してください。</li>
</ul>
</li>
<li>ディスクのストレージが不足していなくても、左側の列にエラーメッセージが表示される場合は、<a href="/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket"> サポートチケットを送信 </a> します。</li>
</ul>
<ul>
<li>サポートナレッジベースの <a href="https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsuite-tracking-indices-causes-problems-with-elasticsearch.html?lang=ja">ElasticSuite トラッキングインデックスが原因でElasticsearchに関する問題が発生する </a> を参照してください。
</li>
</ul>
</td>
</tr>
<tr>
<td><code>Curl</code> エラー</td>
<td><code>curl</code> コマンドを実行してElasticsearchの正常性を確認すると、<code>curl -m1 localhost:9200/_cluster/health?pretty</code> （または <code>curl -m1 elasticsearch.internal:9200/_cluster/health?pretty</code> スターターアカウントの場合）次のエラーが発生します：<i> エラー：curl: （7） localhost ポート 9200 への接続に失敗しました：接続が拒否されました </i> </td>
</tr>
<tr>
<td>コマンドラインエラー</td>
<td><code>$ bin/magento indexer:reindex catalogsearch_fulltext</code> を実行すると、次のエラーが発生します。<i> カタログ検索インデクサープロセスが不明なエラーを処理します：
        クラスター内にアクティブなノードが見つかりません </i>
</td>
</tr>
<tr>
<td>製品ページのエラー
</td>
<td><i>リクエストの処理中にエラーが発生しました。
      セキュリティ上の理由から、例外印刷はデフォルトで無効になっています</code></i>
</tr>
</table>
