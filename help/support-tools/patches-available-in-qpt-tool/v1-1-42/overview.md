---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.1.42'
description: ここでは、 [!DNL Quality Patches Tool]  （QPT） v1.1.42 で使用可能なパッチによって修正された問題について詳しく説明します。
feature: Tools and External Services
role: Admin, Developer
exl-id: 49f7ebd6-7a5f-49da-8fac-c3c2b73b52c1
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 概要：[!DNL Quality Patches Tool] （QPT） v1.1.42

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.1.42 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.1.42 には、次のパッチが含まれています。

1. **ACSD-53658**：製品データがストア表示で適切 *[!UICONTROL Recently Viewed]* 更新されない問題を修正しました。
1. **ACSD-54626**:GraphQLを介して `NUMBER_OF_SKUS` 属性を持つ新しい発注書ルール（`createPurchaseOrderApprovalRule`）を作成できない問題を修正しました。
1. **ACSD-53845**:`consumer max_messages` = 0 の場合の MySQL 接続タイムアウトの問題を修正しました。
1. **ACSD-54890**：ディスクの容量が不足しているために `aggregate_sales_report_bestsellers_data` が原因で MySQL エラーが発生 `/tmp` る問題を修正しました。
1. **ACSD-55112**：検証を行わずに「*[!UICONTROL Submit review]*」ボタンを複数回クリックできる問題 [!DNL Google reCAPTCHA v3] 修正。
1. **ACSD-54264**：エラーメッセージ *リクエストされた属性を更新できない。 行 ID:store_id* は、顧客が別のストアビューから交渉可能な見積もりでチェックアウトしようとすると表示されます。
1. **ACSD-54418**：動的に価格設定されたバンドルの各子製品に、誤って固定額の割引額が適用される問題を修正しました。
1. **ACSD-55238**：空の製品メタ説明を保存する際の問題を修正しました。
1. **ACSD-54966**：以前の注文が失敗した場合に、顧客ごとの使用が制限されているクーポンコードを再利用できない問題を修正しました。
1. **ACSD-54060**：製品が、別の範囲に割り当てられた別の製品の子である場合、制限付き管理者が製品を保存できない問題を修正しました。
1. **ACSD-48910**：複数のソースに割り当てられたバンドル製品が、数量が 0 以外の場合でも、注文が請求および出荷された後に在庫切れになる問題を修正します。
1. **ACSD-55381**:GraphQLを介して B2B *[!UICONTROL Requisition list]* ーバーから `configurable_product_option_uid` フィールドと `configurable_product_option_value_uid` フィールドに対してクエリを実行する際に発生する内部サーバーエラーを修正しました。
1. **ACSD-55628**：会社登録フォームにファイルをアップロードし、ストアフロントの顧客属性のファイルを置き換える問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。
