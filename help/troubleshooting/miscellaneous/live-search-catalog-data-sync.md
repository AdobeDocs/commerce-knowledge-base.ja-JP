---
title: ライブ検索カタログが同期されていません
description: この記事では、ライブサーチ拡張機能を使用する際にカタログデータが正しく同期されないAdobe Commerceの問題に対する解決策を提供します。
exl-id: cd2e602f-b2c7-4ecf-874f-ec5f99ae1900
feature: Catalog Management, Search
role: Developer
source-git-commit: beca5aa3fa796e4b12afc4882024db718b65ac0c
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# ライブ検索カタログが同期されていません

この記事では、ライブサーチ拡張機能を使用する際にカタログデータが正しく同期されないAdobe Commerceの問題に対する解決策を提供します。

## 影響を受ける製品とバージョン

* ライブサーチ拡張機能がインストールされたAdobe Commerce 2.4.x

## イシュー

カタログデータが正しく同期されていないか、新しい商品が追加されましたが、検索結果に表示されません。 `var/log/exception.log`で次のエラーが発生する場合もあります。

`Magento_LiveSearch: An error occurred in search backend. {"result":{"errors":[{"message":"Exception while fetching data (/productSearch) : No index was found for this request"}]}}`

>[!NOTE]
>
>テーブル名`catalog_data_exporter_products`と`catalog_data_exporter_product_attributes`は、[!DNL Live Search] バージョン 4.2.1の時点で`cde_products_feed`と`cde_product_attributes_feed`と呼ばれるようになりました。 4.2.1より前のバージョンのマーチャントの場合は、古いテーブル名`catalog_data_exporter_products`と`catalog_data_exporter_product_attributes`のデータを探します。

<u>複製する手順</u>

1. Adobe Commerce インスタンスのライブサーチを設定して接続する（[&#x200B; ライブサーチのインストール/API キーの設定](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#configure-api-keys)をユーザードキュメントで参照）。
1. 30分後、ユーザードキュメントの「[&#x200B; ライブサーチのインストール/書き出しを検証](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#verify-export)」の説明に従って、書き出されたカタログデータを確認します。
1. 30分後、ユーザードキュメントの[&#x200B; ライブサーチのインストール/接続のテスト &#x200B;](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#test-connection)で説明されているように、接続をテストします。

Or

1. カタログに新商品を追加します。
1. Magento インデクサー+ cronを実行してデータをバックエンドサービスに同期させた時点から15 ～ 20分後に、製品名またはその他の検索可能な属性を使用して検索クエリを実行してみてください。

<u>期待される結果</u>

* エクスポートしたカタログデータは検証可能です
* 接続が成功しました
* 検索結果に新しい商品が表示されます。

<u>実際の結果</u>

書き出されたカタログを検証できないか、API キーが変更されたため、接続が確立されません。

## Solution

カタログの同期に関する問題を修正するには、いくつかの方法があります。

### 変更が適用されるのを待ちます

設定して接続すると、ES （Elasticsearch）のインデックスが作成され、検索結果が返されるまでに30分以上かかることがあります。 その後の1回限りの製品アップデートは、数分以内にインデックス化される予定です。

### 特定のSKUの製品データの同期

製品データが特定のSKUに対して正しく同期されていない場合は、次の操作を行います。

1. 次の[!DNL SQL] クエリを使用して、`feed_data`列に期待するデータがあることを確認してください。 また、`modified_at` タイムスタンプを書き留めます。

   ```sql
   SELECT * FROM cde_products_feed WHERE json_extract(feed_data, '$.sku') = '<your_sku>' AND json_extract(feed_data, '$.storeViewCode') = '<your_ store_view_code>';
   ```

   例：

   ```sql
   SELECT * FROM cde_products_feed WHERE json_extract(feed_data, '$.sku') = '24-MB04' AND json_extract(feed_data, '$.storeViewCode') = 'default';
   ```

1. 正しいデータが表示されない場合は、次のコマンドを使用してインデックスを再作成し、手順1で[!DNL SQL] クエリを再実行してデータを検証します。

   ```bash
   bin/magento indexer:reindex cde_products_feed
   ```

1. それでも正しいデータが表示されない場合は、[&#x200B; サポートチケットを作成してください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)。

### 最後の製品エクスポートのタイムスタンプを確認する

1. `cde_products_feed`に正しいデータが表示された場合は、次の[!DNL SQL] クエリを使用して、前回の書き出しのタイムスタンプを確認します。 `modified_at` タイムスタンプの後にする必要があります：

   ```sql
   select * from scopes_website_data_exporter;
   ```

1. タイムスタンプが古い場合は、次のcron実行を待つか、次のコマンドを使用して自分でトリガーできます。

   ```bash
   bin/magento cron:run --group=saas_data_exporter
   ```

1. `<>`時間（増分更新の時間）待ちます。 それでもデータが表示されない場合は、[&#x200B; サポートチケットを作成してください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)。

### 特定の属性コードを同期

製品属性データが特定の属性コードに対して正しく同期されない場合は、次の操作を行います。

1. 次の[!DNL SQL] クエリを使用して、`feed_data`列に期待するデータがあることを確認してください。 また、`modified_at` タイムスタンプを書き留めます。

   ```sql
   select * from cde_product_attributes_feed where json_extract(feed_data, '$.attributeCode') = '<your_attribute_code>' and store_view_code = '<your_ store_view_code>';
   ```

1. 正しいデータが表示されない場合は、次のコマンドを使用してインデックスを再作成し、手順1の[!DNL SQL] クエリを再実行してデータを検証します。

   ```bash
   bin/magento indexer:reindex cde_product_attributes_feed
   ```

1. それでも正しいデータが表示されない場合は、[&#x200B; サポートチケットを作成してください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)。

### 最後の製品属性エクスポートのタイムスタンプを確認する

`cde_product_attributes_feed`に正しいデータが表示される場合：

1. 次の[!DNL SQL] クエリを使用して、前回の書き出しのタイムスタンプを確認します。 `modified_at` タイムスタンプの後にする必要があります。

   ```sql
   select * from scopes_website_data_exporter;
   ```

1. タイムスタンプが古い場合は、次のcron実行を待つか、次のコマンドを使用して自分でトリガーできます。

   ```bash
   bin/magento cron:run --group=saas_data_exporter
   ```

1. 15～20分待ちます（増分更新の時間）。 それでもデータが表示されない場合は、[&#x200B; サポートチケットを作成してください](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)。

### API設定の変更後に同期

（既知の問題） API設定を変更した結果、データスペース IDが変更され、カタログの変更が同期されていないことが判明した場合は、次のコマンドを実行してフィードを再同期します。

```
bin/magento saas:resync --feed productattributes --cleanup-feed
bin/magento saas:resync --feed products --cleanup-feed
bin/magento saas:resync --feed scopesCustomerGroup --cleanup-feed
bin/magento saas:resync --feed scopesWebsite --cleanup-feed
bin/magento saas:resync --feed prices --cleanup-feed
bin/magento saas:resync --feed productOverrides --cleanup-feed
bin/magento saas:resync --feed variants --cleanup-feed
bin/magento saas:resync --feed categories --cleanup-feed
bin/magento saas:resync --feed categoryPermissions --cleanup-feed
```

[&#x200B; ライブ検索インデックスの再インデックスをリクエストするために、サポートリクエスト &#x200B;](https://experienceleague.adobe.com/home?support-tab=home#support)を送信します。 問題の説明に、**[!UICONTROL System]** > **[!UICONTROL Services]** > **[!UICONTROL Commerce Services Connector]**&#x200B;の下の管理パネルにあるデータスペース/環境IDを含めます。

>[!IMPORTANT]
>他の場合に`--cleanup-feed` オプションを使用すると、データの損失やデータ同期の問題が発生する可能性があります。  新しい空の環境がある場合、Adobe チームがデータスペースのクリーンアップ処理を完了した後、または[—dry-run](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-export-cli-commands#--dry-run) オプションを指定して`saas:resync` コマンドを実行した場合にのみ使用してください。 他の場合に`--cleanup-feed` オプションを使用すると、データの損失やデータ同期の問題が発生する可能性があります。

## 関連トピックス

* [&#x200B; オンボーディングライブサーチ &#x200B;](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/onboarding-overview.html) （ユーザードキュメント）
* [&#x200B; ログを確認し、Adobe Commerce SaaS データ書き出しと同期のトラブルシューティング（](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/logs-troubleshooting/troubleshooting-logging)）（Adobe Commerce SaaS データ書き出しガイド）
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
