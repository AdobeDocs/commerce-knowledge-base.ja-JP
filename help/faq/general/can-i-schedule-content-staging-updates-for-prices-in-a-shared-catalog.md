---
title: 共有カタログの価格に関するコンテンツステージングの更新をスケジュールできますか？
description: Adobe Commerceでは、共有カタログ内の1つ以上の商品の価格更新（[Content Staging] （https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html））のスケジュール機能は提供されていません。
exl-id: 5482326f-54c2-4efc-8e5e-6d075ee5be55
feature: Catalog Management, Customer Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: deedbb4d-f1b7-58ea-a34a-de1f481f9d4c
    internal-label: Customer Service
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%
---
# 共有カタログの価格に関するコンテンツステージングの更新をスケジュールできますか？

Adobe Commerceでは、共有カタログ内の1つ以上の商品の価格更新（[ コンテンツステージング ](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html)）をスケジュールする機能を提供していません。

つまり、Commerce管理パネルの「**価格設定と構造を設定**」メニューから直接価格更新をスケジュールすることはできません（このメニューには「**新しい更新をスケジュール**」ボタンはありません）。

それでも、代替方法を使用して、次の価格の更新をスケジュールすることができます。

* 顧客グループ
* 製品の基本価格

## 顧客グループの価格の更新スケジュール

1. 新しい製品アップデートのスケジュールを[開始](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging-scheduled-update.html)します。
1. 「**価格**」フィールドまでスクロールし、「**詳細価格**」をクリックします。

   ![advanced_pricing.png](assets/advanced_pricing.png){width="600"}

1. **顧客グループ価格セクション**&#x200B;で、必要な顧客グループを選択し、更新された価格を設定します。

   ![customer_group_price.png](assets/customer_group_price.png){width="700"}

1. 更新のスケジュールを通常どおりに完了します。

このワークフローでは、1つの製品の価格のみを更新できます。一括価格の更新は利用できません。

覚えておいてほしいのは、共有カタログでは顧客グループの価格を利用することです。

**関連ドキュメント**

* ユーザーガイドの[更新のスケジュール設定（コンテンツステージング） ](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging-scheduled-update.html)。
* ユーザーガイドの[詳細価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)。

## 基準価格の予定価格の更新

関連記事を参照してください。[基本価格の変更が共有カタログ価格に与える影響は？](/help/faq/general/base-price-change-affect-on-shared-catalog-price.md) サポートナレッジベースに記載されています。
