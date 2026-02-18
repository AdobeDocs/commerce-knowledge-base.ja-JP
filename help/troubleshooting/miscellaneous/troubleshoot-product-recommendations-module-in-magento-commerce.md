---
title: Adobe Commerceの [!UICONTROL Product Recommendations] モジュールのトラブルシューティング
description: この記事では、Adobe Commerceの [!UICONTROL Product Recommendations] モジュールに関するトラブルシューティングの提案について説明します。
exl-id: 431ee31e-eb5b-400c-9c99-cc86613453d7
feature: Cache, Compliance, Extensions, Marketing Tools, Personalization, Products, Recommendations
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Adobe Commerceの [!UICONTROL Product Recommendations] モジュールのトラブルシューティング

この記事では、のトラブルシューティングの提案について説明します

```php
magento/product-recommendations
```

モジュールとその依存関係

```php
saas-export
```

モジュール :Adobe Commerceで [!UICONTROL Product Recommendations] ツールを使用するには、両方のモジュールを動作させる必要があります。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.4 - 2.4.7

## 製品レコメンデーションモジュールのトラブルシューティング

を設定している場合

```php
magento/product-recommendations
```

モジュールは正しく作成されました（開発者向けドキュメントで [[!UICONTROL Product Recommendations - Install and Configure]](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/product-recommendations/getting-started/install-configure) を確認してください）。ただし、レコメンデーションが表示されません。次をお試しください。

* 行動データを収集するのに十分な時間がモジュールにない可能性があります。 システムを 24 時間実行して、データの収集を開始できるようにします。 行動データを必要としないレコメンデーションタイプのデプロイを検討します（例：「*その他の関連リソース*」）。

* 設定したレコメンデーションが表示されない場合は、ユーザーのレコメンデーションを作成するのに十分なデータがない可能性があります。

* [!DNL SaaS] Data Space または [!DNL API] Key が有効であることを確認します。 製品レコメンデーションの初期化中に、[!DNL SaaS] Data Space または [!DNL API] キーを指定した後にエラーが発生した場合は、（ユーザーガイドの） [[!DNL SaaS] Data Space and [!DNL API] key](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/services/saas) を正しく入力したことを確認します。 [!DNL MageID] と [!DNL API] キーが確実にリンクされるようにするには、[!DNL MageID] を所有するユーザー（通常はAdobe Commerce ライセンスを所有するユーザー）が、[!DNL API] キーを生成するユーザーと同じユーザーである必要があります。 使用された [!DNL MageID] を変更する必要がある場合は、[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) します。

>[!NOTE]
>
>[**[!UICONTROL Cookie Restriction Mode]**](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law) （ユーザーガイド内）が *有効* になっている場合、Adobe Commerceは、買い物客が同意するまで行動データを収集しません。**[!UICONTROL Cookie Restriction Mode]**&#x200B;が *無効* になっている場合、Adobe Commerceはデフォルトで行動データを収集します。

## カタログ [!DNL SaaS] 書き出しモジュール

カタログの書き出しに関連する問題 [!DNL SaaS] ついて（

```php
saas-export
```

） モジュール：

1. （開発者向けドキュメントで） [[!DNL cron]](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) ジョブが実行されていることを確認します。
1. （開発者向けドキュメントで） [[!UICONTROL indexers]](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers) が実行されていること、    ```php    Product Feed    ```    [!UICONTROL indexer] はに設定されています。    ```php    Update by Schedule    ```    .
1. モジュールが *有効* になっていることを確認します。 この    ```php    saas-export    ```    metapackage は以下のモジュールをインストールします。これらのモジュールは全て *有効* でなければなりません。    ```php    "magento/module-catalog-data-exporter"      "magento/module-catalog-inventory-data-exporter"      "magento/module-catalog-url-rewrite-data-exporter"      "magento/module-configurable-product-data-exporter"      "magento/module-data-exporter"      "magento/module-saas-catalog"    ```
1. （開発者向けドキュメントの [logs](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/enable-logging) を確認します。 上記のモジュールに関連するエラーがないことを確認します。
1. [!UICONTROL Configuration cache] を更新します。 **システム**/**ツール**/**キャッシュ管理** に移動し、[!UICONTROL Configuration cache] をクリアします。
1. `cde_products_products_feed` データベーステーブルにデータがあることを確認します。

   >[!NOTE]
   >
   >そのテーブルが見つからない場合は、`catalog_data_exporter_products` のテーブルを確認します。 テーブル名は、[!DNL Data Export] バージョン 103.3.0 リリースで変更されました。

## イベント

開発者向けドキュメントの [&#x200B; イベント収集の検証 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/product-recommendations/getting-started/verify) では、Adobe Commerceに送信される行動イベントについて説明しています。

## 関連資料

* 開発者向けドキュメントの [Product Recommendations 管理者向け開発 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/product-recommendations/developer/development-overview)
* 製品レコメンデーションガイドの [&#x200B; 製品レコメンデーションの概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/product-recommendations/overview)
* 製品レコメンデーションガイドの [&#x200B; 製品レコメンデーションの作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/product-recommendations/admin/create)
* [&#x200B; Data Export Guide の &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/saas-data-export/troubleshooting-logging) ログの確認とトラブルシューティング [!DNL SaaS]
* [[!DNL SaaS]  Services 用Adobe Commerce データ書き出しガイドの &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/saas-data-export/release-notes) データ書き出し拡張機能のリリースノート [!DNL SaaS]
* Commerce実装プレイブックの [&#x200B; データベーステーブルを変更する際のベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)

