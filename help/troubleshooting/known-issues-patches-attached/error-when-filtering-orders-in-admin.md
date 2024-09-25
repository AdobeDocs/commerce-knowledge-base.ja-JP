---
title: 管理者で注文をフィルター中にエラーが発生する
description: この記事では、「Integrity constraint violation 1052 Column 'created_at' where clause is ambiguous」というメッセージが表示され、管理者の注文を日付別にフィルタリングしようとするとエラーが発生するAdobe Commerce問題のパッチを提供します。
feature: Orders
role: Developer
source-git-commit: e5eb65b23afaed4658f8576c747f11a31a8ec1aa
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 管理者で注文をフィルター中にエラーが発生する

この記事では、管理者の注文を日付でフィルター処理しようとするとエラーが発生するAdobe Commerce問題に対するパッチを提供します。このパッチに *Integrity constraint violation: 1052 Column &#39;created_at&#39; where 句があいまいである* というメッセージが表示されます。

## 影響を受けるバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.7

## 問題

管理画面の注文を日付でフィルタリングすると、エラーが返されます。

exception.log には、次が表示されます。

```SQL
report.CRITICAL: PDOException: SQLSTATE[23000]: Integrity constraint violation: 1052 Column 'created_at' in where clause is ambiguous in /path/to/magento/vendor/magento/framework/DB/Statement/Pdo/Mysql.php:90
```

<u> 再現手順：</u>

1. **[!UICONTROL Admin]**/**[!UICONTROL Sales]**/**[!UICONTROL Orders]** に移動します。
   * グリッド **[!UICONTROL Purchase Date Ascending]** 順序を設定する、または
   * フィルターで **[!UICONTROL Purchase Date Filter]** を設定します。

1. *デフォルトのビューの処理で問題が発生し、フィルターが元の状態に復元されました* というエラーが表示されます。

## 原因：

[!DNL PayPal Braintree] モジュールに問題があります。

## 解決策

この問題を解決するには、この記事に添付されているパッチを適用します。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[bundle_3357_filter_order_in_admin_by_date_patch.zip](assets/bundle-3357-unable-to-filter-order-in-admin-by-date.zip)

パッチは、影響を受けるすべてのバージョンとエディションと互換性があります。

## パッチの適用方法

手順については、サポート技術情報の [Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。
