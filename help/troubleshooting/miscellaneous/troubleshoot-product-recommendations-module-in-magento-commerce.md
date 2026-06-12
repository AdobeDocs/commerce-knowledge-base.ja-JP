---
title: Adobe Commerceの[!UICONTROL Product Recommendations] モジュールのトラブルシューティング
description: この記事では、Adobe Commerceの[!UICONTROL Product Recommendations] モジュールのトラブルシューティングに関する推奨事項について説明します。
exl-id: 431ee31e-eb5b-400c-9c99-cc86613453d7
feature: Cache, Compliance, Extensions, Marketing Tools, Personalization, Products, Recommendations
role: Developer
source-git-commit: 48b929f6fdf0bf8745ec03c8faa8b07bf5b3e5c3
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Adobe Commerceの[!UICONTROL Product Recommendations] モジュールのトラブルシューティング

この記事では、のトラブルシューティングの提案について説明します。

```php
magento/product-recommendations
```

モジュールとその依存関係

```php
saas-export
```

Adobe Commerceで[!UICONTROL Product Recommendations] ツールを使用するには、両方のモジュールが動作している必要があります。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.4 - 2.4.7

## product-recommendations モジュールのトラブルシューティング

を設定した場合

```php
magento/product-recommendations
```

モジュールを正しく設定してください（開発者用ドキュメントの[[!UICONTROL Product Recommendations - Install and Configure]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/getting-started/install-configure)を確認してください）。 レコメンデーションが表示されない場合は、次をお試しください。

* モジュールに行動データを収集する十分な時間がない可能性があります。 システムを24時間稼働させ、データ収集を開始できるようにします。 「*詳細はこちら*」など、行動データを必要としないレコメンデーションタイプをデプロイすることを検討してください。

* 設定したレコメンデーションが表示されない場合、ユーザー向けのレコメンデーションを構築するのに十分なデータがまだ存在しない可能性があります。

* [!DNL SaaS] データ スペースまたは[!DNL API] キーが有効であることを確認してください。 製品レコメンデーションの初期化中に[!DNL SaaS] データ スペースまたは[!DNL API] キーを指定した後にエラーが発生した場合は、[[!DNL SaaS]  データ スペースと [!DNL API]  キー](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)を（ユーザーガイド内）正しく入力したことを確認してください。 [!DNL MageID]と[!DNL API] キーがリンクされていることを確認するには、[!DNL MageID]を所有するユーザー（通常はAdobe Commerce ライセンスを所有するユーザー）が、[!DNL API] キーを生成する同じユーザーである必要があります。 使用した[!DNL MageID]を変更する必要がある場合は、[ サポートチケット ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)を送信します。

>[!NOTE]
>
>[**[!UICONTROL Cookie Restriction Mode]**](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law) （ユーザーガイド内）が&#x200B;*有効*の場合、Adobe Commerceは買い物客の同意を得るまで行動データを収集しません。**[!UICONTROL Cookie Restriction Mode]**が&#x200B;*無効*の場合、Adobe Commerceはデフォルトで行動データを収集します。

## カタログ [!DNL SaaS]書き出しモジュール

カタログ [!DNL SaaS]の書き出しに関連する問題（

```php
saas-export
```

） モジュール：

1. [[!DNL cron]](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) （開発者用ドキュメント）ジョブが実行中であることを確認します。
1. [[!UICONTROL indexers]](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) （開発ドキュメント）が実行されており、`Product Feed` [!UICONTROL indexer]が`Update by Schedule`に設定されていることを確認してください。
1. モジュールが&#x200B;*有効*&#x200B;であることを確認してください。 `saas-export` メタパッケージは次のモジュールをインストールします。これらはすべて&#x200B;*有効*&#x200B;である必要があります。
   * `magento/module-catalog-data-exporter`
   * `magento/module-catalog-inventory-data-exporter`
   * `magento/module-catalog-url-rewrite-data-exporter`
   * `magento/module-configurable-product-data-exporter`
   * `magento/module-data-exporter`
   * `magento/module-saas-catalog`
1. [logs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/enable-logging)を確認してください（開発者用ドキュメント内）。 上記のモジュールに関連するエラーがないことを確認してください。
1. [!UICONTROL Configuration cache]を更新します。 **システム** > **ツール** > **キャッシュ管理**&#x200B;に移動し、[!UICONTROL Configuration cache]をクリアします。
1. `cde_products_products_feed` データベーステーブルにデータがあることを確認します。

   >[!NOTE]
   >
   >そのテーブルが見つからない場合は、`catalog_data_exporter_products` テーブルを確認してください。 テーブル名は[!DNL Data Export] バージョン 103.3.0 リリースで変更されました。

## イベント

[Verify Event Collection](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/getting-started/verify)は、開発者向けドキュメントで、Adobe Commerceに送信される動作イベントについて説明しています。

## 関連トピックス

* 開発者ドキュメントの[製品レコメンデーション管理者開発](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/developer/development-overview)
* 製品レコメンデーションガイドの[製品レコメンデーションの概要](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/overview)
* 商品レコメンデーションガイドの[商品レコメンデーションの作成](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/admin/create)
* [!DNL SaaS] データ書き出しガイドの[ ログの確認と](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/logs-troubleshooting/troubleshooting-logging)のトラブルシューティング
* [!DNL SaaS] サービスのAdobe Commerce データ書き出しガイドの[[!DNL SaaS]  データ書き出し拡張機能リリースノート ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/saas-data-export/release-notes)
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
