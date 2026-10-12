---
title: 特定の製品を探す際に数千もの結果を得る
description: この記事では、特定の製品を探しているときに数千もの検索結果が表示される問題の解決策を提供します。
feature: Quotes, Search, Returns
role: Developer, Admin
exl-id: 0eccf212-96be-4ea5-9e6e-95f27d7d9f92
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 792a7e9b-6519-5e99-a913-56c3dd2408da
    internal-label: Quotes
  - id: ac07462c-732c-5c1c-947b-4ce533b4fcfb
    internal-label: Returns
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%
---
# 特定の製品を探す際に数千もの結果を得る

この記事では、特定の製品を探しているときに数千もの検索結果が表示される問題の解決策を提供します。

## 影響を受ける製品とバージョン

* [!DNL ElasticSearch]がインストールされているすべてのバージョンをAdobe Commerce

## イシュー

特定の商品（例：*WSH12-32-Red*）を探していますが、検索で類似した商品が大量に返されます。

## 解決策

[!DNL ElasticSearch]のフルテキスト検索の性質は、完全一致ではなく、関連性に基づいています。 そのため、最も関連性の高い一致（完全一致のSKUなど）が最初に注文されます。

ただし、検索語（完全一致）と完全に一致する検索結果が必要な場合は、検索クエリに引用符を使用する必要があります。 例えば、引用符を含まない&#x200B;*WSH12-32-Red*&#x200B;のクエリでは、複数の結果が返され、結果の最初に正確な一致（*SKU WSH12-32-Red*&#x200B;の製品）が表示されます。 しかし、引用符で囲まれたクエリ *&quot;WSH12-32-Red&quot;*&#x200B;は、完全一致の結果を1つだけ返します。
