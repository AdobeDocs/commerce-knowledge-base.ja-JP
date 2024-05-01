---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.34'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.34。
feature: Tools and External Services
role: Admin
exl-id: 79998832-26cb-4c11-a505-08c3382f86d4
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.34

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.34。

QPT v1.1.34 には、次のパッチが含まれています。

1. **ACSD-52277**：管理者で新しい注文を作成する際に、ストア表示を選択した後、管理者ユーザーが適切にリダイレクトされない問題を修正しました。
1. **ACSD-50813**：管理者が SKU にスラッシュを含むバンドル製品をで追加できない問題を修正しました [!UICONTROL Add Products by SKU] 管理注文に対する機能。
1. **ACSD-51630**：大量のシステムメッセージが原因で管理ページのダウンロードが遅くなる問題を修正しました。
1. **ACSD-51853**：を使用した際に、コピーしたテキストスタイルが適用されない問題を修正しました [!DNL Page Builder].
1. **ACSD-52160**：買い物かご価格ルールに対する製品検証結果が、ルール条件に基づいて適切に評価されなかった問題を修正しました *買い物かごで項目が見つかった/見つからなかった場合、これらの条件のすべてを満たす*.
1. **ACSD-51636**：必要な役割と権限をすべて持っているにもかかわらず、管理者が顧客アカウントセクションから新しいユーザーを追加できない問題を修正しました。
1. **ACSD-51739**：でエラーが返される場合の問題を修正しました `structure_id` 次でリクエストされた `CompanyTeam` GraphQL リクエスト。
1. **ACSD-51857**：のパフォーマンスが低下する問題を修正しました `aggregate_sales_report_bestsellers_data` cron レポートが大きな影響を受ける `sales_order` および `sales_order_item` データベーステーブル。
1. **ACSD-48448**：注文のキャンセル中に競合状態の問題が発生し、でエントリが重複する問題を修正しました *inventory_reservation* テーブル。
1. **ACSD-52689**：に画像をアップロードできない問題を修正しました [!DNL Amazon S3] rest API を使用したストレージ。

左側のメニューを使用して、特定のパッチページに移動します。
