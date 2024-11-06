---
title: ページビルダーに製品Recommendationsが表示されない
description: ここでは、「製品のRecommendations」オプションがページビルダーに表示されない問題の解決策について説明します。
exl-id: e96a446b-2e64-47a6-ac1b-e73183da9fb8
feature: Page Builder, Configuration, Personalization, Products, Recommendations
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# ページビルダーに製品Recommendationsが表示されない

ここでは、「製品のRecommendations」オプションがページビルダーに表示されない問題の解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法）

## 問題

製品Recommendationsオプションがページビルダーに表示されない。

## 原因：

ページビルダーには、製品Recommendationsを追加するオプションはありません。 ページビルダー用の製品Recommendationsはオプションのモジュールで、個別にインストールされます。

## 解決策

1. 次のコマンドを実行して、モジュールが個別にインストールされているかどうかを確認します。`composer show magento/module-page-builder-product-recommendations`
1. *Package magento/module-page-builder-product-recommendations not found* というメッセージが返される場合は、コマンド `composer require magento/module-page-builder-product-recommendations` を実行してインストールする必要があります。

ページビルダーで製品Recommendationsを有効にすると、ページビルダーで作成した任意のコンテンツに [ レコメンデーションユニットを追加 ](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html) できます。

## 関連資料

* ユーザーガイドの [ コンテンツを追加 – 製品Recommendations](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html)。
* 開発者向けドキュメントの [Product Recommendationsのインストールと設定 ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/product-recommendations/getting-started/install-configure) を参照してください。
* [Adobe Commerce ユーザーガイド ](https://experienceleague.adobe.com/en/docs/commerce-admin/user-guides/home)
