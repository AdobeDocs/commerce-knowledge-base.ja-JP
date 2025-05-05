---
title: 「ダッシュボード [!DNL Live Search] 検索結果のランキングが正しくありません」
description: この記事では、 [!DNL Live Search]  ダッシュボードのデータが正しくない場合や、検索結果のランキングが期待どおりでない場合のトラブルシューティング情報を提供します。
feature: Admin Workspace, Categories, Search
role: Developer
source-git-commit: 4c1199c31f83d7c2aaf28e259d63473779bf2efe
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# ダッシュボ [!DNL Live Search] ドと検索結果のランキングが正しくありません

[!DNL Live Search] ダッシュボードに表示されるデータが正しくない場合や、[ 検索結果のランキング ](https://experienceleague.adobe.com/ja/docs/commerce-merchant-services/live-search/live-search-admin/category-merch#ranking-strategies) が期待どおりでない場合は、考えられる理由により次を参照してください。

* `productView` イベントの製品コンテキストの `topLevelSku` フィールドがありません。 これにより、空のコンバージョンや、その他の予期しない指標が発生します。

* `add-to-cart` イベントには、`productContext` フィールドが設定されておらず、値が入力されていません。

* 環境のタイプが正しくありません。 例えば、環境が *[!UICONTROL Production]* ではなく *[!UICONTROL Testing]* に設定されている場合です。 詳しくは、[ ストアフロントコンテキスト ](https://github.com/adobe/commerce-events/blob/main/examples/events/example-contexts/mock-storefront-context.md) を参照してください。

* [search-product-click](https://github.com/adobe/commerce-events/blob/main/examples/events/search-product-click.md) イベントに検索結果のコンテキストがありません。
