---
title: 共有カタログの価格に対してコンテンツのステージングの更新をスケジュールすることはできますか？
description: Adobe Commerceには、共有カタログ内の 1 つ以上の商品の価格アップデート （[ コンテンツのステージング ] （https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html））をスケジュールする機能はありません。
exl-id: 5482326f-54c2-4efc-8e5e-6d075ee5be55
feature: Catalog Management, Customer Service
source-git-commit: c3120f7df24e105b082df6544ab82241d6b6851f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 共有カタログの価格に対してコンテンツのステージングの更新をスケジュールすることはできますか？

Adobe Commerceは、共有カタログ内の 1 つ以上の商品の価格アップデート（[ コンテンツステージング ](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html)）をスケジュールする機能を提供していません。

つまり、Commerce管理パネルの **価格と構造を設定** メニューから直接価格の更新をスケジュールすることはできません（このメニューには **新規更新をスケジュール** ボタンはありません）。

それでも、別の方法を使用して、次の項目の価格アップデートをスケジュールすることができます。

* 顧客グループ
* 製品の基本価格

## 顧客グループの価格更新をスケジュール

1. [ 新しい製品アップデートのスケジュール設定 ](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging-scheduled-update.html) を開始します。
1. 「**価格**」フィールドまでスクロールし、「**詳細価格**」をクリックします。

   ![advanced_pricing.png](assets/advanced_pricing.png){width="600"}

1. **顧客グループ価格セクション** で、必要な顧客グループを選択し、更新された価格を設定します。

   ![customer_group_price.png](assets/customer_group_price.png){width="700"}

1. 通常どおり更新のスケジュールを完了します。

このワークフローでは、1 つの製品の価格のみを更新できます。一括価格更新はできません。

注意：共有カタログは、顧客グループの価格を利用します。

**関連ドキュメント**

* ユーザーガイドの [ 更新のスケジュール （コンテンツのステージング） ](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging-scheduled-update.html)。
* ユーザーガイドの [ 詳細価格 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)。

## 基本価格の予定価格更新

関連記事：[ 基本価格の変更は共有カタログ価格にどのような影響を与えるか？](/help/faq/general/base-price-change-affect-on-shared-catalog-price.md) しくは、サポートナレッジベースを参照してください。
