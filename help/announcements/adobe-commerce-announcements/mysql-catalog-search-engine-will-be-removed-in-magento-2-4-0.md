---
title: MySQL カタログ検索エンジンは、Adobe Commerce 2.4.0 で削除されます
description: Adobe Commerce オンプレミス、Adobe Commerce on cloud infrastructure、Magento Open Source 2.4.0 は、今後数か月でリリースされる予定です。 Adobe Commerce オンプレミスおよびMagento Open Source バージョン 2.4.0 Elasticsearch 6.x または 7.x の場合、必須のコンポーネントとなり、MySQL 検索エンジンは削除されます。 クラウドインフラストラクチャー上のAdobe Commerceでは、既にElasticsearchが必要です。
exl-id: 717be515-3cbf-42e9-9b72-caf11b8c3771
feature: Catalog Management, Search, Services
role: Admin
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# MySQL カタログ検索エンジンは、Adobe Commerce 2.4.0 で削除されます

Adobe Commerce オンプレミス、Adobe Commerce on cloud infrastructure、Magento Open Source 2.4.0 は、今後数か月でリリースされる予定です。 Adobe Commerce オンプレミスおよびMagento Open Source バージョン 2.4.0 Elasticsearch 6.x または 7.x の場合、必須のコンポーネントとなり、MySQL 検索エンジンは削除されます。 クラウドインフラストラクチャー上のAdobe Commerceでは、既にElasticsearchが必要です。

>[!WARNING]
>
>アップグレードする前にElasticsearch 6/7 をインストールまたは設定しないと、Adobe Commerceで重大な問題が発生する可能性があります。 なお、クラウドインフラストラクチャー上のAdobe Commerceのサービスアップグレードは、インフラストラクチャチームに 48 営業時間前に通知しなければ、実稼動環境にプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある [ サポートチケットを送信 ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)48 時間前に、必要なサービスアップグレードの詳細と、アップグレードプロセスを開始する時刻を指定します。

MySQL 検索エンジンが廃止された理由は、Elasticsearchが優れた検索機能とカタログパフォーマンスの最適化を提供しているためです。

## 影響を受ける製品とバージョン：

* Adobe Commerce オンプレミス v2.4.0
* Magento Open Source v2.4.0

## アップグレード：

<table style="height: 164px; width: 632.2px;">
<tbody>
<tr>
<td class="wysiwyg-text-align-center" style="width: 133px;"><strong>検索エンジン</strong></td>
<td class="wysiwyg-text-align-center" style="width: 478.2px;"><strong>アクション</strong></td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" style="width: 133px;">MySQL</td>
<td style="width: 478.2px;">Elasticsearchをインストールします。 開発者向けドキュメントの <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/search/overview-search">Elasticsearchのインストールと設定 </a> を参照してください。</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" style="width: 133px;">Elasticsearch（バージョンはリストされていません）</td>
<td style="width: 478.2px;">Elasticsearch 2 を使用しているので、Elasticsearch 7 （推奨）または 6 にアップデートする必要があります。 詳しくは、開発者向けドキュメントの <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/search/overview-search#es-upgrade6">Elasticsearchのアップグレード </a> および <a href="https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/search/configure-search-engine">Elasticsearchを使用するためのCommerceの設定 </a> を参照してください。</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" style="width: 133px;">ELASTICSEARCH5</td>
<td style="width: 478.2px;">Elasticsearch 5 は <a href="https://www.elastic.co/support/eol"> 提供が終了 </a> し、Adobe Commerce 2.4.0 で非推奨（廃止予定）になりました。Elasticsearch 7 （推奨）または 6 にアップデートします。</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" style="width: 133px;">Elasticsearch 6 または 7</td>
<td style="width: 478.2px;">Adobe Commerce 2.4.0 にアップグレードする前に、追加の手順を実行する必要はありません。</td>
</tr>
<tr>
<td class="wysiwyg-text-align-center" style="width: 133px;">サードパーティの拡張機能</td>
<td style="width: 478.2px;">Elasticsearchをインストールする必要はありません。 Adobe Commerceでは、使用している拡張機能がAdobe Commerce 2.4.0 と完全に互換性があるかどうかを確認する場合は、検索エンジンのベンダーにお問い合わせください。</td>
</tr>
</tbody>
</table>

## インストール：

Adobe Commerce オンプレミスおよびMagento Open Source 2.4.0 がリリースされると、Elasticsearchは必須のコンポーネントになるので、バージョン 2.4.0 をインストールする前に、Elasticsearch ホストをセットアップして設定する必要があります。開発者向けドキュメントの [Elasticsearchのインストールと設定 ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/search/overview-search) を参照してください。

デフォルトでは、Adobe Commerce検索はElasticsearch 7 を検索エンジンとして使用し、localhost:9200 にあるサーバーへの接続を試みます。 Elasticsearch 6.x もサポートされています。 設定がデフォルトと一致しない場合は、データベース接続を設定する場合と同様に、`setup:install` に渡される引数を使用してこれらの設定を設定できます。

例：`setup:install --elasticsearch-host=es.mystore.com`

インストール時に、Elasticsearch接続がチェックされ、Adobe CommerceがElasticsearch ホストに接続できない場合はインストールが失敗します。 この場合は、Elasticsearchが起動して実行されていること、および正しい接続パラメーターが指定されていることを確認します。
