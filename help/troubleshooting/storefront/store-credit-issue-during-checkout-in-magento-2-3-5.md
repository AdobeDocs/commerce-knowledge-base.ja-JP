---
title: Adobe Commerce 2.3.5 のチェックアウト中の店舗のクレジットの問題
description: この記事では、Adobe Commerce 2.3.5 のチェックアウト中に、店舗のクレジット使用状況を選択して後で削除した後、チェックアウト中に買い物客がエラーが発生する既知の店舗クレジット関連の問題を回避します。 永続的な修正は、Adobe Commerce 2.3.6 で利用できるようになります。
exl-id: a0cca226-4d95-40b3-bd37-f13d28591366
feature: Checkout, Orders, Storefront
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Adobe Commerce 2.3.5 のチェックアウト中の店舗のクレジットの問題

この記事では、Adobe Commerce 2.3.5 のチェックアウト中に、店舗のクレジット使用状況を選択して後で削除した後、チェックアウト中に買い物客がエラーが発生する既知の店舗クレジット関連の問題を回避します。 永続的な修正は、Adobe Commerce 2.3.6 で利用できるようになります。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.5
* クラウドインフラストラクチャー 2.3.5 上のAdobe Commerce

## 問題

<u> 再現手順 </u>:

1. 顧客は商品を買い物かごに追加し、チェックアウトに進みます。
1. 顧客が支払方法として店舗クレジットを指定します。
1. 顧客が店舗クレジットを削除し、支払い方法を変更します。
1. お客様はチェックアウトを通じて進行します。

<u> 期待される結果 </u>:

すべての注文情報が正しく表示されます。

<u> 実際の結果 </u>:

Adobe Commerceが、「注文」ページの「注文の概要」セクションでエラーをスローする。

## 解決策

お客様は注文ページを更新でき、注文概要の情報は正しく読み込まれます。 修正は、2020 年 Q4 にリリースされるAdobe Commerce 2.3.6 で利用できるようになります。

## 関連資料

サポートナレッジベースのAdobe Commerce 2.3.5 の既知の問題に関する記事：

* [Adobe Commerce 2.3.5 でバーチャル商品が正しく処理されない複数出荷の注文](/help/troubleshooting/miscellaneous/magento-2-3-5-known-issue-virtual-product-multi-ship-orders.md)

* [Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.5 および 2.3.5-p1 における国の支払い方法の問題](/help/troubleshooting/known-issues-patches-attached/magento-2-3-5-2-3-5-p1-patch-country-payment-issue.md)

* [Adobe Commerceでユーザーにログインを求めるが、無効なリンクが表示される](/help/troubleshooting/known-issues-patches-attached/magento-prompts-customers-log-in-invalid-link.md)

* [Adobe Commerce 2.3.5 の一括アクション製品数の既知の問題](/help/troubleshooting/miscellaneous/bulk-action-product-count-known-issue-in-magento-2-3-5.md)

* [Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ](/help/troubleshooting/payments/patch-for-amazon-pay-checkout-issue-in-magento-2-3-5-p1.md)

* [Adobe Commerce 2.3.5 の製品比較の問題](/help/troubleshooting/storefront/product-comparison-known-issue-in-magento-2-3-5.md)

開発者向けドキュメントでは、

* [Adobe Commerce 2.3.5 の既知の問題 ](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#known-issues)
