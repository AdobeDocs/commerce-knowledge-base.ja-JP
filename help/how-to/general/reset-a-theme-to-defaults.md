---
title: テーマをデフォルトにリセットする
description: テーマをカスタマイズしてストアを開発する際に発生する可能性のある問題によっては、Commerce管理者からアクセスできない場合があります。 管理者にアクセスしなくても、テーマのデフォルトをクリアしてリセットできます。 テーマをクリアすると、デフォルトのLuma テーマが適用されます。
exl-id: 86304dd5-f448-4dcc-ad07-04ecc6c85b6d
feature: Cache
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%
---
# テーマをデフォルトにリセットする

テーマをカスタマイズしてストアを開発する際に発生する可能性のある問題によっては、Commerce管理者からアクセスできない場合があります。 管理者にアクセスしなくても、テーマのデフォルトをクリアしてリセットできます。 テーマをクリアすると、デフォルトのLuma テーマが適用されます。

Adobe Commerce（すべてのデプロイメント）とMagento Open Source コンポーネント（モジュール、テーマ、言語パッケージ）を開発する場合、急速に変化する環境では、特定のディレクトリとキャッシュを定期的にクリアする必要があります。 そうしないと、コードは例外で実行され、適切に機能しません。 詳しくは、開発者用ドキュメントの「[開発中にディレクトリをクリア &#x200B;](https://developer.adobe.com/commerce/php/development/components/clear-directories/)」を参照してください。

## 環境とテクノロジー

* Adobe Commerce オンプレミス
* Adobe Commerce on cloud infrastructure
* Magento Open Source

## 前提条件

* データベースツール

## 手順

ストアテーマをリセットする必要があるものの、管理パネルにアクセスできない場合は、次の操作を行うことで、データベース内でストアテーマをリセットできます。

1. [phpMyAdmin](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/optional-software#phpmyadmin)などのデータベースツールを使用するか、コマンドラインからDBに手動でアクセスして、次のSQL クエリを実行します：`UPDATE core_config_data SET value=NULL WHERE path='design/theme/theme_id'`
1. 次のディレクトリをクリアします。
   * `pub/static/frontend`
   * `var/view_preprocessing`
   * `var/cache`
   * `var/page_cache`

この方法では、ストアビューレベルにテーマが設定されず、ストアフロントページをリロードすると、デフォルトのLuma テーマが適用されます。

## 追加情報

* 開発中に[&#x200B; ディレクトリをクリアする](https://developer.adobe.com/commerce/php/development/components/clear-directories/)詳しくは、開発者ドキュメントを参照してください
