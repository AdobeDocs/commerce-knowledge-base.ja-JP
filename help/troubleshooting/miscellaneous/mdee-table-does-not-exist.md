---
title: 変更ログテーブルが存在しない場合に、更新されていないデータの in [!DNL Commerce Data Exporter] feed および  [!DNL cron] logs エラーを修正しました
description: この記事では、購読での間違ったビュー ID の使用によって発生したデータ同期の問題を修正するソリューショ  [!DNL Commerce Data Exporter mview]  を説明します。
feature: Data Import/Export, Saas, Logs
role: Developer
source-git-commit: cf87b5f1280a2d1d23c7ace37616feb337b5142f
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# [!DNL Commerce Data Exporter] フィードで更新されない修正データと、変更ログテーブルを含む [!DNL cron] ログエラーが存在しません

この記事では、[!DNL Data Exporter] [[!DNL Mview]](https://developer.adobe.com/commerce/php/development/components/indexing/#mview) サブスクリプションで間違ったビュー ID を使用することで発生したデータ同期の問題を修正する方法について説明します。 [!DNL Mview] サブスクリプションは、データベーステーブルの変更を追跡するために使用されます。

## 影響を受ける製品とバージョン

カスタムコードがデータ書き出し機能（`commerce-data-exporter` または `saas-exporter`）に適用されたAdobe Commerce インスタンス。 このエラーは、インストールされている [[!DNL SaaS]  データエクスポートのバージョンが 103.3.0](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/saas-data-export/release-notes#release-6) 以降で、コードが `catalog_data_exporter_products` インデックスを直接参照する場合に発生します。

## 問題

マーチャントは、データフィード [!DNL Data Exporter] ーブルのカタログにデータ更新がないことに気付き、[!DNL cron] のジョブのログに次のエラーが表示される場合があります。

```
[2024-05-27T19:00:04.627604+00:00] report.ERROR: Cron Job indexer_clean_all_changelogs has an error: Table catalog_data_exporter_products_cl does not exist. Statistics: {"sum":0,"count":1,"realmem":0,"emalloc":0,"realmem_start":305135616,"emalloc_start":283210384} [] [] 
```

## 原因：

[!DNL Commerce Data Export] [ バージョン 103.3.0](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/saas-data-export/release-notes#release-9) リリースでフィードテーブル、インデックス、変更ログテーブルの名前が変更されたので、[!DNL Commerce Data Export] 拡張機能を使用するカスタム拡張機能の [!DNL Mview] サブスクリプションが正しく機能しない場合があります。

この場合、*テーブルが存在しません* エラーは、`catalog_data_exporter` テーブル名が `cde_products_feed` に変更され、[!DNL Data Exporter Mview] サブスクリプションで古い名前を参照するカスタムコードがあるために発生します。

## 解決策

カスタマイズした拡張機能で、[!DNL Mview] 設定ファイル（```./etc/mview.xml```）を編集して、`catalog_data_exporter_products` テーブル名を *`cde_products_feed`* に変更します。

次の例は、[!DNL Mview] 購読によって追跡されるテーブルを指定するコードを示しています。

```
<view id="cde_products_feed" class="Magento\CatalogDataExporter\Model\Indexer\ProductFeedIndexer" group="indexer">
     <subscriptions>
         <table name="custom_table" entity_column="product_id" />
     </subscriptions>
</view>
```

## 関連資料

[!DNL SaaS] Services 用Adobe Commerce データ書き出しガイドの [[!DNL SaaS]  データ書き出し拡張機能のリリースノート ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/saas-data-export/release-notes)。
