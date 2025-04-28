---
title: ライブ検索カタログが同期されていません
description: この記事では、Adobe Commerce拡張機能を使用するとカタログデータが正しく同期されない Live Search の問題の解決策について説明します。
exl-id: cd2e602f-b2c7-4ecf-874f-ec5f99ae1900
feature: Catalog Management, Search
role: Developer
source-git-commit: fec99ebd6b03f2dc1b70c0ea388935dc5e60ad57
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# ライブ検索カタログが同期されていません

この記事では、Adobe Commerce拡張機能を使用するとカタログデータが正しく同期されない Live Search の問題の解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.x （Live Search Extension がインストールされている場合）

## 問題

カタログデータが正しく同期されていないか、新しい製品が追加されたが検索結果に表示されません。 また、`var/log/exception.log` で次のエラーが発生する場合もあります。

`Magento_LiveSearch: An error occurred in search backend. {"result":{"errors":[{"message":"Exception while fetching data (/productSearch) : No index was found for this request"}]}}`

>[!NOTE]
>
>[!DNL Live Search] バージョン 4.2.1 以降、テーブル名 `catalog_data_exporter_products` と `catalog_data_exporter_product_attributes` は `cde_products_feed` と `cde_product_attributes_feed` になりました。4.2.1 より前のバージョンのマーチャントの場合、古いテーブル名 `catalog_data_exporter_products` および `catalog_data_exporter_product_attributes` でデータを探します。

<u> 再現手順 </u>

1. アドビのユーザードキュメントの [Live Search のインストール/API キーの設定 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#configure-api-keys) に従って、Adobe Commerce インスタンスの Live Search を設定して接続します。
1. 30 分後、ユーザードキュメントの [Live Search のインストール/書き出しの確認 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#verify-export) の説明に従って、書き出されたカタログデータを確認します。
1. 30 分後、ユーザードキュメントの [Live Search のインストール/接続のテスト ](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#test-connection) の説明に従って接続をテストします。

Or

1. カタログに新しい商品を追加します。
1. Magento インデクサーと cron がデータをバックエンドサービスに同期させるために実行してから 15～20 分後に、製品名またはその他の検索可能な属性を使用して検索クエリを実行してみてください。

<u> 期待される結果 </u>

* 書き出されたカタログ データを確認できます
* 接続に成功しました
* 検索結果に新製品が表示されます。

<u> 実際の結果 </u>

API キーが変更されたため、エクスポートされたカタログを確認できないか、接続が確立されていません。

## 解決策

カタログの同期に関する問題を修正する方法はいくつかあります。

### 変更が適用されるのを待ちます

設定して接続すると、ES （Elasticsearch）のインデックスが作成され、検索結果が返されるまで、30 分以上かかる場合があります。 その後の 1 回限りの製品アップデートは、数分以内にインデックスが作成される予定です。

### 特定の SKU の製品データを同期

特定の SKU に対して製品データが正しく同期されていない場合は、次の操作をおこないます。

1. 次の [!DNL SQL] クエリを使用して、`feed_data` の列に目的のデータが入力されていることを確認します。 また、`modified_at` タイムスタンプもメモしておきます。

   ```sql
   SELECT * FROM cde_products_feed WHERE json_extract(feed_data, '$.sku') = '<your_sku>' AND json_extract(feed_data, '$.storeViewCode') = '<your_ store_view_code>';
   ```

   例：

   ```sql
   SELECT * FROM cde_products_feed WHERE json_extract(feed_data, '$.sku') = '24-MB04' AND json_extract(feed_data, '$.storeViewCode') = 'default';
   ```

1. 正しいデータが表示されない場合は、次のコマンドを使用して再インデックスを実行し、手順 1 で [!DNL SQL] クエリを再実行してデータを確認します。

   ```bash
   bin/magento indexer:reindex cde_products_feed
   ```

1. それでも正しいデータが表示されない場合は、[ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。

### 前回の製品書き出しのタイムスタンプを確認

1. `cde_products_feed` に正しいデータが表示された場合は、次の [!DNL SQL] クエリを使用して、最後の書き出しのタイムスタンプを確認します。 `modified_at` タイムスタンプの後にする必要があります。

   ```sql
   select * from scopes_website_data_exporter;
   ```

1. タイムスタンプが古い場合は、次の cron 実行を待つか、次のコマンドを使用して自分でトリガーすることができます。

   ```bash
   bin/magento cron:run --group=saas_data_exporter
   ```

1. `<>` 時間（増分更新の時間）待ちます。 それでもデータが表示されない場合は、[ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。

### 特定の属性コードを同期

特定の属性コードに対して製品属性データが正しく同期されていない場合は、次の操作を行います。

1. 次の [!DNL SQL] クエリを使用して、`feed_data` の列に目的のデータが入力されていることを確認します。 また、`modified_at` タイムスタンプもメモしておきます。

   ```sql
   select * from cde_product_attributes_feed where json_extract(feed_data, '$.attributeCode') = '<your_attribute_code>' and store_view_code = '<your_ store_view_code>';
   ```

1. 正しいデータが表示されない場合は、次のコマンドを使用して再インデックスを実行し、手順 1 で [!DNL SQL] クエリを再実行してデータを検証します。

   ```bash
   bin/magento indexer:reindex cde_product_attributes_feed
   ```

1. それでも正しいデータが表示されない場合は、[ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) します。

### 最後の製品属性エクスポートのタイムスタンプを確認します

`cde_product_attributes_feed` に正しいデータが表示される場合：

1. 次の [!DNL SQL] クエリを使用して、前回の書き出しのタイムスタンプを確認します。 `modified_at` タイムスタンプの後にする必要があります。

   ```sql
   select * from scopes_website_data_exporter;
   ```

1. タイムスタンプが古い場合は、次の cron 実行を待つか、次のコマンドを使用して自分でトリガーすることができます。

   ```bash
   bin/magento cron:run --group=saas_data_exporter
   ```

1. 15～20 分待ちます（増分更新のための時間）。 それでもデータが表示されない場合は、[ サポートチケットを作成 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) してください。

### API 設定の変更後に同期

（既知の問題） API 設定を変更した場合、結果としてデータ領域 ID が変更され、カタログの変更が同期されなくなっている場合は、次のコマンドを実行してフィードを再同期します。

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

ライブサーチのインデックス再作成をリクエストする [ サポートリクエストを送信 ](https://experienceleague.adobe.com/home?support-tab=home#support) します。 問題の説明で、管理パネルの **[!UICONTROL System]**/**[!UICONTROL Services]**/**[!UICONTROL Commerce Services Connector]** の下にあるデータスペース/環境 ID を含めます。

>[!IMPORTANT]
>`--cleanup-feed` オプションは、API 設定を更新した場合、または [—dry-run](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/data-export-cli-commands#--dry-run) オプションを使用して `saas:resync` コマンドを実行した場合にのみ使用します。 その他の場合に `--cleanup-feed` オプションを使用すると、データの損失やデータ同期の問題が発生します。

## 関連資料

* ユーザードキュメントの [ オンボーディング Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/onboarding-overview.html)
* Adobe Commerce SaaS データ書き出しガイドの [ ログの確認とAdobe Commerce SaaS データの書き出しと同期のトラブルシューティング ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/saas-data-export/troubleshooting-logging)
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
