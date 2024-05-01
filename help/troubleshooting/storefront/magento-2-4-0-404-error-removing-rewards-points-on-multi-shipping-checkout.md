---
title: 「Adobe Commerce 2.4.0：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する」
description: この記事では、複数出荷のチェックアウトページで報酬ポイントを削除する際に発生した「*404 Not Found*」 Web ページエラーに対する、Adobe Commerce 2.4.0 の既知の問題の回避策を説明します。 現在、複数配送のチェックアウトページで、注文の支払いに使用した報酬ポイントを削除しようとすると、報酬ポイントのキャンセルに成功した代わりに「*404 Not Found*」ページが表示されます。 この問題は、Adobe Commerce 2.4.1 パッチリリースで解決されます。
exl-id: 59de4b3d-af28-4ae8-8f55-4ec958e6ee8b
feature: B2B, Checkout, Orders, Rewards, Shipping/Delivery, Storefront
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Adobe Commerce 2.4.0：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する

この記事では、「」に対するAdobe Commerce 2.4.0 の既知の問題の回避策を説明します&#x200B;*404 が見つかりません*「複数配送のチェックアウトページで報酬ポイントを削除する際に、web ページエラーが発生する。 現在、複数配送のチェックアウトページで、注文の支払いに使用した報酬ポイントを削除しようとすると、「*404 が見つかりません* 「成功した報酬ポイントキャンセルの代わりに、ページが表示されます。 この問題は、Adobe Commerce 2.4.1 パッチリリースで解決されます。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.0 （すべてのデプロイメント方法）

## 問題

<u>再現手順</u>

1. ストアフロントに移動し、顧客としてログインします。
1. 少なくとも 2 つの製品をに追加 **ショッピングカート**.
1. を開きます **ミニカート**.
1. 「」をクリックします **買い物かごの表示と編集** リンク。
1. 「」をクリックします **複数のアドレスを使用してチェックアウト** リンク。
1. 配送先住所の選択 **複数のアドレスに発送** ページ。
1. 「」をクリックします **配送情報に移動** ボタン。
1. 「」を選択します **定率 – 固定配送方法** （アドレスごとに）。
1. 「」をクリックします **請求情報の続行** ボタン。
1. を確認します **報酬ポイントを使用** チェックボックス： **請求情報** ページ。
1. 「」をクリックします **注文を確認に移動** ボタン。
1. 「」をクリックします **削除** 報酬ポイントを削除するアドレスへのリンク。

<u>期待される結果</u>

* この **ショッピングカート** ページが表示されます。
* 「*この注文から報酬ポイントを削除しました。* 「メッセージが表示されます。

<u>実際の結果</u>

A ``*404 が見つかりません* 「エラーページが表示されます。

## 回避策

回避策は、購入者をに戻すことです。 **カート** から報酬ポイントを削除します **カート** web ページ。 この問題は、2020 年 Q4 のリリースが予定されているAdobe Commerce バージョン 2.4.1 パッチで修正される予定です。

## 関連資料

* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
