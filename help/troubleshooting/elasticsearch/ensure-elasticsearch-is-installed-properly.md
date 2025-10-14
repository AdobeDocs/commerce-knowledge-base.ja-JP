---
title: Elasticsearchが正しくインストールされていることを確認します。
description: この文書では、Elasticsearch（ES）のインストールと設定の誤りに起因する問題の解決策について説明します。
exl-id: d2c5971c-4db4-4857-ae79-970313bce981
feature: Install
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Elasticsearchが正しくインストールされていることを確認します。

この文書では、Elasticsearch（ES）のインストールと設定の誤りに起因する問題の解決策について説明します。

>[!WARNING]
>
>クラウドインフラストラクチャー上のAdobe Commerceの場合、インフラストラクチャチームに 48 営業時間前に通知しない限り、実稼動環境にサービスアップグレードをプッシュすることはできません。 実稼動環境のダウンタイムを最小限に抑え、目的の期間内に設定を更新できるインフラストラクチャサポートエンジニアを確保する必要があるので、これが必要になります。 そのため、変更を実稼動環境で行う必要がある場合は、48 時間前に [&#x200B; サポートチケットを送信 &#x200B;](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、必要なサービスアップグレードの詳細を説明し、アップグレードプロセスを開始する時刻を指定します。

## ElasticsearchバージョンとAdobe Commerceとの互換性

* Adobe CommerceのオンプレミスおよびAdobe Commerceのクラウドインフラストラクチャ：
   * v2.2.3 以降は、ES 5.x をサポート
   * v2.2.8+および v2.3.1+は、ES 6.x をサポートしています。
   * ES v2.x および v5.x は、[&#x200B; 提供終了 &#x200B;](https://www.elastic.co/support/eol) が理由で推奨されていません。 ただし、Adobe Commerce v2.3.1 を使用していて、ES 2.x または ES 5.x を使用する場合は、[Elasticsearch php クライアントを変更する &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) 必要があります。
* Magento Open Source v2.3.0 以降では、ES 5.x および 6.x がサポートされています（ただし 6.x をお勧めします）。

## 問題

次の現象は、Elasticsearchが正しく設定されていないことを示しています。

* `Error: No alive nodes in your cluster` – このエラーはAdobe Commerce ログに表示される場合があります。
   * `var/log/system.log`
   * `var/log/support_report.log`
   * `var/log/cron.log`
   * `var/log/exception.log`
   * または、プロンプトで表示されます（例：再インデックスを実行する場合）。
* ElasticsearchのバージョンがAdobe Commerceの現在のバージョンと互換性がないことを示すエラー（これは、クラウドインフラストラクチャ上のAdobe Commerceに固有のエラーです）。

  ```
  [YYYY-MM-DD HH:MM:SS] CRITICAL: Fix configuration with given suggestions:    - Elasticsearch version #<version> is not compatible with current version of magento    Upgrade elasticsearch version to ~5.0
  ```

ここで、*version* はクラウド上で動作しているElasticsearchサービスです。

## 原因：

Elasticsearchが正しくインストールされていません。 これは次のような原因が考えられます。

* 設定ファイルの誤字。
* 設定ファイル内のバージョンが、その環境にインストールされているElasticsearchのどのバージョンとも一致しません。
* 環境に正しくインストールされ、設定ファイル内で正しく設定されているが、現在インストールされているAdobe Commerceのバージョンではサポートされていないバージョン。

## 解決策

Elasticsearchを正しく設定するには：

* クラウドインフラストラクチャー上のAdobe Commerceのマーチャントは、開発者向けドキュメントの [Elasticsearchサービスの設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/service/elasticsearch) の手順に従うことができます。
* Adobe Commerceのオンプレミス環境およびMagento Open Source上のマーチャントは、開発者向けドキュメントの [Elasticsearchのインストールと設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/search/overview-search) の手順に従うことができます。

Elasticsearchを設定したら、正しく設定されていることを確認します。

1. サーバーにログインします。
1. コマンドを実行した出力に含まれているElasticsearchのバージョン番号（2.x、5.x または 6.x）を確認します。`curl -XGET <Elasticsearch hostname>:<Elasticsearch server port>` 例えば、クラウドインフラストラクチャー上のAdobe Commerceでは次のようになります。`curl -XGET localhost:9200`
1. 次のコマンドを実行して、クラウドインフラストラクチャ設定のAdobe Commerceで設定されていることを確認します。`php bin/magento config:show catalog/search`
1. `catalog/search/engine` をチェックし、Elasticsearchのバージョン番号と一致することを確認します。 例えば、クラウドインフラストラクチャー上のAdobe Commerceでは次のようになります。
   * Elasticsearch 5.X - elasticsearch5
   * Elasticsearch 6.X - elasticsearch6
   * Elasticsearch 2.X - elasticsearch
1. `index_prefix` を確認します。 複数の環境がある場合は、それらの `index_prefix` の値が異なることを確認します。
