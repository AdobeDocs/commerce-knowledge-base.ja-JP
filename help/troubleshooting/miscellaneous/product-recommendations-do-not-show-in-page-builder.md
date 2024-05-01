---
title: ページビルダーに製品Recommendationsが表示されない
description: ここでは、「製品のRecommendations」オプションがページビルダーに表示されない問題の解決策について説明します。
exl-id: e96a446b-2e64-47a6-ac1b-e73183da9fb8
feature: Page Builder, Configuration, Personalization, Products, Recommendations
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
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

1. 次のコマンドを実行して、モジュールが個別にインストールされているかどうかを確認します。 `composer show magento/module-page-builder-product-recommendations`
1. 次のメッセージが返される場合： *magento/module-page-builder-product-recommendations パッケージが見つかりません*&#x200B;をインストールするには、コマンドを実行する必要があります。 `composer require magento/module-page-builder-product-recommendations`

ページビルダーで製品Recommendationsを有効にすると、次のことが可能になります [レコメンデーションユニットの追加](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html) をページビルダーで作成されたすべてのコンテンツに適用します。

## 関連資料

* [コンテンツを追加 – 製品Recommendations](https://experienceleague.adobe.com/docs/commerce-admin/page-builder/add-content/recommendations.html) を参照してください。
* [製品Recommendationsのインストールと設定](https://devdocs.magento.com/recommendations/install-configure.html) 開発者向けドキュメントを参照してください。
* [Adobe Commerce ユーザーガイド](https://docs.magento.com/user-guide/)
