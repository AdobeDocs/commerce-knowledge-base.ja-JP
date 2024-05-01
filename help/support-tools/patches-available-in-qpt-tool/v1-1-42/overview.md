---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.42'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.42.
feature: Tools and External Services
role: Admin, Developer
exl-id: 49f7ebd6-7a5f-49da-8fac-c3c2b73b52c1
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.42

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.42.

QPT v1.1.42 には、次のパッチが含まれています。

1. **ACSD-53658**：の問題を修正します *[!UICONTROL Recently Viewed]* 商品データがストア表示で正しく更新されない。
1. **ACSD-54626**：新しい発注書ルールを作成できない問題を修正しました（`createPurchaseOrderApprovalRule`）に設定する必要があります。 `NUMBER_OF_SKUS` 属性（GraphQL経由）。
1. **ACSD-53845**：次の場合の MySQL 接続タイムアウトの問題を修正します `consumer max_messages` = 0。
1. **ACSD-54890**：の問題を修正します `aggregate_sales_report_bestsellers_data` が原因で MySQL エラーが発生する理由 `/tmp` ディスクの空き領域が不足しています。
1. **ACSD-55112**：が発生した問題を修正します *[!UICONTROL Submit review]* ボタンは、次の操作を行わずに複数回クリックできます [!DNL Google reCAPTCHA v3] 検証。
1. **ACSD-54264**：エラーメッセージが表示される問題を修正します *リクエストされた属性を更新することはできません。 行 ID: store_id* 顧客が別のストア表示から交渉可能な見積もりでチェックアウトを試みたときに表示されます。
1. **ACSD-54418**：動的に価格設定されるバンドルの各子製品に誤って固定額の割引額が適用される問題を修正しました。
1. **ACSD-55238**：空の製品メタ説明を保存する際の問題を修正しました。
1. **ACSD-54966**：以前の注文が失敗した場合に、顧客ごとの使用が制限されているクーポンコードを再利用できない問題を修正しました。
1. **ACSD-54060**：製品が、別の範囲に割り当てられた別の製品の子である場合、制限付き管理者が製品を保存できない問題を修正しました。
1. **ACSD-48910**：注文が請求および出荷された後、複数のソースに割り当てられたバンドル製品が在庫切れになる問題を、数量が 0 以外の場合でも修正します。
1. **ACSD-55381**：クエリ時の内部サーバーエラーを修正します `configurable_product_option_uid` および `configurable_product_option_value_uid` b2B からのフィールド *[!UICONTROL Requisition list]* GraphQL経由
1. **ACSD-55628**：会社登録フォーム上にファイルをアップロードし、ストアフロントの顧客属性のファイルを置き換える問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。
