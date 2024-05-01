---
title: Adobe Commerceの製品Recommendationsモジュールのトラブルシューティング
description: この記事では、のトラブルシューティングの提案について説明します
exl-id: 431ee31e-eb5b-400c-9c99-cc86613453d7
feature: Cache, Compliance, Extensions, Marketing Tools, Personalization, Products, Recommendations
role: Developer
source-git-commit: b20ad74194bacb09116131f4a8da1006da75738a
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Commerceの製品Recommendationsモジュールのトラブルシューティング

この記事では、のトラブルシューティングの提案について説明します

```php
magento/product-recommendations
```

モジュールとその依存関係

```php
saas-export
```

モジュール :Adobe Commerceで Product Recommendations ツールを使用するには、両方のモジュールを動作させる必要があります。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.4 - 2.4.7

## 製品レコメンデーションモジュールのトラブルシューティング

を設定している場合

```php
magento/product-recommendations
```

モジュールが正しい（チェック [製品Recommendations - Recommendationsのインストールと設定](https://devdocs.magento.com/recommendations/install-configure.html) 開発者向けドキュメントを参照してください）が、レコメンデーションが表示されません。次をお試しください。

* 行動データを収集するのに十分な時間がモジュールにない可能性があります。 システムを 24 時間実行して、データの収集を開始できるようにします。 行動データを必要としないレコメンデーションタイプのデプロイを検討します（例：「More like this」）。

* 設定したレコメンデーションが表示されない場合は、ユーザーのレコメンデーションを作成するのに十分なデータがない可能性があります。

* SaaS データ空間または API キーが有効であることを確認してください。 製品レコメンデーションの初期化中に、SaaS データ領域または API キーを指定した後にエラーが発生した場合は、を入力したことを確認します [SaaS データ空間と API キー](https://docs.magento.com/user-guide/configuration/services/saas.html) （ユーザーガイド内）正しく。 MageID と API キーが確実にリンクされるようにするには、MageID を所有するユーザー（通常はAdobe Commerce ライセンスを所有するユーザー）が、API キーを生成するユーザーと同じである必要があります。 使用した MageID を変更する必要がある場合、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

>[!NOTE]
>
>次の場合 [Cookie 制限モード](https://docs.magento.com/m2/ce/user_guide/stores/compliance-cookie-restriction-mode.html) （ユーザーガイドで）が有効になっている場合、買い物客が同意するまで、Adobe Commerceは行動データを収集しません。 Cookie 制限モードが無効になっている場合、Adobe Commerceはデフォルトで行動データを収集します。

## カタログ SaaS エクスポート モジュール

カタログの SaaS 書き出しに関連する問題（

```php
saas-export
```

） モジュール：

1. 「」を確認します [cron](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-cron.html) （開発者向けドキュメントで）ジョブを実行中です。
1. 「」を確認します [インデクサー](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-index.html) （開発者向けドキュメントで）を実行しており、    ```php    Product Feed    ```    インデクサーはに設定されています。    ```php    Update by Schedule    ```    .
1. モジュールが有効になっていることを確認します。 この    ```php    saas-export    ```    metapackage は以下のモジュールをインストールします。これらのモジュールを全て有効にしておく必要があります：    ```php    "magento/module-catalog-data-exporter"      "magento/module-catalog-inventory-data-exporter"      "magento/module-catalog-url-rewrite-data-exporter"      "magento/module-configurable-product-data-exporter"      "magento/module-data-exporter"      "magento/module-saas-catalog"    ```
1. を確認します [ログ](https://devdocs.magento.com/guides/v2.3/config-guide/cli/logging.html) （開発者向けドキュメントを参照）。 上記のモジュールに関連するエラーがないことを確認します。
1. 設定キャッシュを更新します。 に移動 **システム** > **ツール** > **キャッシュ管理** 設定キャッシュをクリアします。
1. にデータがあることを確認します    ```php    catalog_data_exporter_products    ```    データベーステーブル。

## イベント

[レコメンデーションイベント](https://devdocs.magento.com/recommendations/verify.html)アドビの開発者向けドキュメントでは、Adobe Commerceに送信される行動イベントについて説明しています。

## 関連資料

* [製品Recommendations – 概要](https://devdocs.magento.com/recommendations/product-recs.html) 開発者向けドキュメントで
* [製品Recommendations - Recommendationsのインストールと設定](https://devdocs.magento.com/recommendations/install-configure.html) 開発者向けドキュメントで
* [マーケティング – 製品Recommendations](https://docs.magento.com/m2/ee/user_guide/marketing/product-recommendations.html) ユーザーガイドの
* [製品Recommendationsを作成](https://docs.magento.com/m2/ee/user_guide/marketing/create-new-rec.html) ユーザーガイドの
