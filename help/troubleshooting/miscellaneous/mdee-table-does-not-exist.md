---
title: ' [!DNL Commerce Data Exporter]  フィードでデータが更新されず、変更ログテーブルを含むエラーが [!DNL cron]  ログに記録されない問題を修正します'
description: この記事では、 [!DNL Commerce Data Exporter mview]  サブスクリプションで間違ったビューIDを使用することで発生するデータ同期の問題を修正するためのソリューションを提供します。
feature: Data Import/Export, Saas, Logs
role: Developer
exl-id: 50f2223b-bfcf-4c3c-b0f1-dbcc4365edc2
source-git-commit: 40766238a7ea748bff86decf75cddec28fe63bb9
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# [!DNL Commerce Data Exporter] フィードでデータが更新されず、[!DNL cron]が変更ログテーブルを持つエラーが存在しません

この記事では、[!DNL Data Exporter] [[!DNL Mview]](https://developer.adobe.com/commerce/php/development/components/indexing/#mview) サブスクリプションで間違ったビューIDを使用することで発生するデータ同期の問題を修正するためのソリューションを提供します。 [!DNL Mview] サブスクリプションは、データベーステーブルの変更を追跡するために使用されます。

## 影響を受ける製品とバージョン

カスタムコードがデータ書き出し機能（`commerce-data-exporter`または`saas-exporter`）に適用されたAdobe Commerce インスタンス。 インストールされている[[!DNL SaaS]  データ書き出しバージョンが103.3.0](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/saas-data-export/release-notes#release-6)以降で、コードが`catalog_data_exporter_products` インデックスを直接参照している場合にエラーが発生します。

## イシュー

マーチャントは、カタログ [!DNL Data Exporter] フィード テーブルにデータ更新が見つからないことがわかり、[!DNL cron] ジョブ ログに次のエラーが表示される場合があります。

```
[2024-05-27T19:00:04.627604+00:00] report.ERROR: Cron Job indexer_clean_all_changelogs has an error: Table catalog_data_exporter_products_cl does not exist. Statistics: {"sum":0,"count":1,"realmem":0,"emalloc":0,"realmem_start":305135616,"emalloc_start":283210384} [] [] 
```

## 原因

[!DNL Commerce Data Export] [&#x200B; バージョン 103.3.0](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/saas-data-export/release-notes#release-9) リリースのフィード テーブル、インデックス、およびログ テーブルの変更の名前の変更により、[!DNL Commerce Data Export]拡張機能を使用するカスタム拡張機能の[!DNL Mview] サブスクリプションが正しく機能しない可能性があります。

この場合、`catalog_data_exporter` テーブル名が`cde_products_feed`に変更され、[!DNL Data Exporter Mview] サブスクリプションで古い名前を参照するカスタムコードが含まれているため、*テーブルが存在しません* エラーが発生します。

## Solution

カスタマイズされた拡張機能で、[!DNL Mview]設定ファイル （`./etc/mview.xml`）を編集して、`catalog_data_exporter_products` テーブル名を&#x200B;*`cde_products_feed`*&#x200B;に変更します。

次の例は、[!DNL Mview] サブスクリプションによって追跡されるテーブルを指定するコードを示しています。

```
<view id="cde_products_feed" class="Magento\CatalogDataExporter\Model\Indexer\ProductFeedIndexer" group="indexer">
     <subscriptions>
         <table name="custom_table" entity_column="product_id" />
     </subscriptions>
</view>
```

## 関連トピックス

* [!DNL SaaS] サービスのAdobe Commerce データ書き出しガイドの[[!DNL SaaS]  データ書き出し拡張機能リリースノート &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/saas-data-export/release-notes)
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
