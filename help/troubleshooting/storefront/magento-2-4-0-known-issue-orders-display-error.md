---
title: 「Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー」
description: 「この記事では、注文の表示エラーに関するAdobe Commerceの既知の問題の回避策を説明します。 ログインしている顧客が**マイアカウント**メニュー（**マイアカウント&gt; マイオーダー**）で注文を確認すると、11 件の注文がある場合に、注文グリッドでページあたりの注文数をページ 2 から 20 に切り替えることができません。 また、1 ページに表示されるように設定されている注文数よりも多くの注文がある場合、注文を含む最後のページに移動すると、1 ページに表示される注文数を変更すると、「注文していません」というエラーメッセージが表示されます。 この問題はAdobe Commerce 2.4.1 で解決されます。'
exl-id: a6d300e1-1cbc-42b9-997d-d72f8765517b
feature: B2B, Categories, Storefront
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー

この記事では、注文の表示エラーに関するAdobe Commerceの既知の問題の回避策を説明します。 ログイン中、お客様はで注文を確認します **マイアカウント** メニュー（**マイアカウント/マイオーダー**）、11 件の注文がある場合、注文グリッドは、ページ 2 からのページあたりの注文数を 20 に切り替えることができません。 また、1 ページに表示するように設定されている注文数よりも多くの注文がある場合、注文を含む最後のページに移動すると、1 ページに表示される注文数を変更すると、次のエラーメッセージが表示されます。 *注文していません*. この問題は、Adobe Commerce 2.4.1 で解決されます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

<u>前提条件</u>

* Adobe Commerce 2.4.0 がインストールされています。
* 少なくとも 1 つのカテゴリと 1 つのシンプルな製品を作成します。

<u>再現手順</u>

1. 製品を使用して 11 の注文を作成します。
1. に移動 **マイアカウント**.
1. に移動 **マイ注文**.
1. 2 番目のページをクリックして、注文グリッドに 11 番目の注文を表示します。
1. を選択 **表示= 1 ページにつき 20** ドロップダウンメニューから。

<u>期待される結果</u>

11 件の注文はすべて、期待どおりに最初のページに表示されます。

<u>実際の結果</u>

この *注文していません* エラーメッセージが表示されます。

## 回避策

回避策は、バイヤーを再オープンすることです **マイ注文** ページを開くと、注文リストが正しく表示されます。 この問題は、2020 年 Q4 のリリースが予定されている次回のリリースであるAdobe Commerce 2.4.1 で修正されます。

## サポートナレッジベースの関連するリーディング

* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
