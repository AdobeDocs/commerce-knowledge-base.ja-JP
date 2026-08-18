---
title: ページビルダーに表示されない商品レコメンデーション
description: この記事では、ページビルダーに商品レコメンデーションオプションが表示されない問題の解決策を提供します。
exl-id: e96a446b-2e64-47a6-ac1b-e73183da9fb8
feature: Page Builder, Configuration, Personalization, Products, Recommendations
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# ページビルダーに表示されない商品レコメンデーション

この記事では、ページビルダーに商品レコメンデーションオプションが表示されない問題の解決策を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）

## イシュー

ページビルダーに「商品レコメンデーション」オプションが表示されない。

## 原因

ページビルダーには、商品レコメンデーションを追加するオプションはありません。 ページビルダーの製品レコメンデーションはオプションのモジュールで、個別にインストールされます。

## Solution

1. 次のコマンドを実行して、モジュールを個別にインストールしたかどうかを確認します：`composer show magento/module-page-builder-product-recommendations`
1. 次のメッセージが返される場合：*Package magento/module-page-builder-product-recommendations not found*、次のコマンドを実行してインストールする必要があります：`composer require magento/module-page-builder-product-recommendations`

ページビルダーで製品レコメンデーションを有効にすると、ページビルダーで作成されたあらゆるコンテンツに[ レコメンデーションユニット ](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html)を追加できるようになります。

## 関連トピックス

* ユーザーガイドの[ コンテンツの追加 – 製品レコメンデーション ](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html)。
* [製品レコメンデーションのインストールと設定](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/getting-started/install-configure)については、開発者ドキュメントをご覧ください。
* [Adobe Commerce ユーザーガイド](https://experienceleague.adobe.com/en/docs/commerce-admin/user-guides/home)
