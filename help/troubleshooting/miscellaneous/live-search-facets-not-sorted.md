---
title: '[!DNL Live Search]個のファセットがアルファベット順に並べ替えられていません'
description: この記事では、[!DNL Live Search] ファセットがアルファベット順に並べ替えられない場合のトラブルシューティング情報を提供します。
feature: Admin Workspace, Categories, Search
role: Developer
exl-id: 59f86727-c2a6-4418-8753-40f7937e059c
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
source-wordcount: '146'
ht-degree: 0%
---
# [!DNL Live Search]個のファセットがアルファベット順に並べ替えられていません

## 影響を受ける製品とバージョン

Adobe Commerce バージョン 2.4.x以降

## イシュー

Adobe Commerceのストアフロントのすべてのファセットは、対応する属性に割り当てられている入力タイプに関係なく、単一選択オプションを使用してアルファベット順に並べ替えられます。

## 回避策

ただし、一部のエッジケースでは、[[!DNL Live Search]  ファセットワークスペース ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/live-search/live-search-admin/facets/faceting-workspace)で設定したアルファベット順にファセットが並べ替えられない場合があります。

回避策として、[!UICONTROL Admin]属性セクションで製品属性を並べ替えることができます。

1. **[!UICONTROL Admin]** サイドバーで、**ストア** > *属性* > **製品**&#x200B;に移動します。
1. テーブルから属性を選択します。

   ![属性リスト ](assets/attribute-list.png)

1. 並べ替える値を持つ属性を開き、**属性情報** > **プロパティ**&#x200B;を選択します。
1. **オプションの管理**&#x200B;で、属性値を並べ替えることができます。

   ![属性を並べ替え](assets/sort-attributes.png)
