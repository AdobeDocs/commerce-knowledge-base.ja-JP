---
title: '[!DNL Live Search] ダッシュボードと検索結果のランキングが正しくありません'
description: この記事では、[!DNL Live Search] ダッシュボードのデータが正しくない場合、または検索結果のランキングが期待どおりでない場合のトラブルシューティング情報を提供します。
feature: Admin Workspace, Categories, Search
role: Developer
exl-id: d4aea1f1-c2c4-45e5-87c8-73069f7c9ffd
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: bb2df8be-afdd-4818-b6b5-95ca1dd3bc3a
    internal-label: Admin workspace
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
    internal-label: Categories
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%
---
# [!DNL Live Search] ダッシュボードと検索結果のランキングが正しくありません

[!DNL Live Search] ダッシュボードに表示されるデータが正しくない場合、または検索結果の[&#x200B; ランキング &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/live-search/live-search-admin/category-merch#ranking-strategies)が期待したものではない場合は、考えられる理由について次を参照してください。

* `productView` イベントの製品コンテキストの`topLevelSku` フィールドがありません。 これにより、空のコンバージョンやその他の予期しない指標が発生します。

* `add-to-cart` イベントには、`productContext` フィールドが設定および入力されていません。

* 環境タイプが正しくありません。 例えば、環境が&#x200B;*[!UICONTROL Production]*&#x200B;ではなく&#x200B;*[!UICONTROL Testing]*&#x200B;に設定されている場合です。 詳しくは、[&#x200B; ストアフロントのコンテキスト &#x200B;](https://github.com/adobe/commerce-events/blob/main/examples/events/example-contexts/mock-storefront-context.md)を参照してください。

* 検索結果コンテキストが[search-product-click](https://github.com/adobe/commerce-events/blob/main/examples/events/search-product-click.md) イベントにありません。
