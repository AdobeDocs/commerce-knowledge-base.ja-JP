---
title: '[!DNL Live Search] ダッシュボードと検索結果のランキングが正しくありません'
description: この記事では、 [!DNL Live Search]  ダッシュボードのデータが正しくない場合、または検索結果のランキングが期待どおりでない場合のトラブルシューティング情報を提供します。
feature: Admin Workspace, Categories, Search
role: Developer
exl-id: d4aea1f1-c2c4-45e5-87c8-73069f7c9ffd
source-git-commit: 9bb839292a120a3dab5151d493f915619dbf5c06
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# [!DNL Live Search] ダッシュボードと検索結果のランキングが正しくありません

[!DNL Live Search] ダッシュボードに表示されるデータが正しくない場合、または検索結果の[&#x200B; ランキング &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/live-search/live-search-admin/category-merch#ranking-strategies)が期待したものではない場合は、考えられる理由について次を参照してください。

* `productView` イベントの製品コンテキストの`topLevelSku` フィールドがありません。 これにより、空のコンバージョンやその他の予期しない指標が発生します。

* `add-to-cart` イベントには、`productContext` フィールドが設定および入力されていません。

* 環境タイプが正しくありません。 例えば、環境が&#x200B;*[!UICONTROL Production]*&#x200B;ではなく&#x200B;*[!UICONTROL Testing]*&#x200B;に設定されている場合です。 詳しくは、[&#x200B; ストアフロントのコンテキスト &#x200B;](https://github.com/adobe/commerce-events/blob/main/examples/events/example-contexts/mock-storefront-context.md)を参照してください。

* 検索結果コンテキストが[search-product-click](https://github.com/adobe/commerce-events/blob/main/examples/events/search-product-click.md) イベントにありません。
