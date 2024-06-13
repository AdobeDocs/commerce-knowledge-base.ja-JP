---
title: テーマをデフォルトにリセット
description: テーマをカスタマイズしてストアを開発する際に発生する可能性のある問題によっては、Commerce管理者からアクセスできない場合があります。 管理者にアクセスすることなく、テーマを消去してデフォルトにリセットできます。 テーマをクリアすると、デフォルトの Luma テーマが適用されます。
exl-id: 86304dd5-f448-4dcc-ad07-04ecc6c85b6d
feature: Cache
source-git-commit: 83b21845cd306336e1cb193a9541478c8a38eea8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# テーマをデフォルトにリセット

テーマをカスタマイズしてストアを開発する際に発生する可能性のある問題によっては、Commerce管理者からアクセスできない場合があります。 管理者にアクセスすることなく、テーマを消去してデフォルトにリセットできます。 テーマをクリアすると、デフォルトの Luma テーマが適用されます。

Adobe Commerce（すべてのデプロイメント）およびMagento Open Sourceコンポーネント（モジュール、テーマおよび言語パッケージ）を開発する際に、急速に変化する環境では特定のディレクトリおよびキャッシュを定期的にクリアする必要があります。 そうしないと、コードは例外で実行され、正しく機能しません。 詳しくは、を参照してください [開発時にディレクトリをクリア](https://devdocs.magento.com/guides/v2.2/howdoi/php/php_clear-dirs.html) 開発者向けドキュメントを参照してください。

## 環境とテクノロジー

* Adobe Commerce オンプレミス
* クラウドインフラストラクチャー上のAdobe Commerce
* Magento Open Source

## 前提条件

* データベースツール

## 手順

ストアテーマをリセットする必要があるが、管理パネルにアクセスできない場合は、次の手順を実行してデータベース内でテーマをリセットできます。

1. 次のようなデータベースツールを使用します [phpMyAdmin](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/optional.html#install-optional-phpmyadmin) または、コマンドラインから手動で DB にアクセスして、次の SQL クエリを実行します。 `UPDATE core_config_data SET value=NULL WHERE path='design/theme/theme_id'`
1. 次のディレクトリをクリアします。
   * `pub/static/frontend`
   * `var/view_preprocessing`
   * `var/cache`
   * `var/page_cache`

これにより、ストア表示レベルでテーマが設定されることはなくなり、ストアのフロントページをリロードすると、デフォルトの Luma テーマが適用されます。

## 追加情報

* [開発時にディレクトリをクリア](https://devdocs.magento.com/guides/v2.2/howdoi/php/php_clear-dirs.html) 開発者向けドキュメントで
