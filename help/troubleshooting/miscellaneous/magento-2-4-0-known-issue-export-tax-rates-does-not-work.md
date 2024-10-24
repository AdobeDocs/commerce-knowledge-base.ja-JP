---
title: Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない
description: この記事では、「**書き出し税率**」ボタンが機能しない、Adobe Commerce 2.4.0 の既知の問題の解決策を提供します。
exl-id: 29a34a1f-d23a-43cb-ac1f-8711ce25fa6c
feature: Data Import/Export, Orders
role: Developer
source-git-commit: a1046621259ea49eab74cd6ba3bba550e0c70283
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の既知の問題 – 輸出税率が機能しない

この記事では、「**輸出税率**」ボタンが機能しない、Adobe Commerce 2.4.0 の既知の問題の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## 問題

<u> 再現手順：</u>

1. Commerce管理パネル/**ストア**/**税務ルール** に移動します。
1. 「**新規税務処理基準の追加**」ボタンをクリックします。
1. 「税率の書き出し **ボタンのテキストをクリック** ます。

   ![magento_export_tax_rates.png](assets/mceclip0.png)

<u> 期待される結果 </u>:

税率を含む `tax_rates.csv` ファイルがダウンロードされます。

<u> 実際の結果 </u>:

.csv ファイルはダウンロードされません。

## 解決策

回避策：

「税率のエクスポート **ボタンの左下にあるボタンをクリックして**`tax_rates.csv` ファイルをエクスポートします。

![magento_export_tax_rates.png](assets/mceclip1.png)

この問題は 2.4.1 パッチで解決される予定です。

## 関連資料

サポートナレッジベースでは、

* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintreeによるお支払い方法が表示されません ](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)。
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しません ](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)。
* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される ](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)。
* [Adobe Commerce 2.4.0 の既知の問題：「選択項目を買い物かごに追加」ボタンが機能しません ](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)。
