---
title: Adobe Commerce 2.3.5 の一括アクション製品数の既知の問題
description: ここでは、Adobe Commerce 2.3.5 の既知の問題について説明します。管理画面での一括アクションの後にマーチャントが受け取る通知に、誤った数の影響を受けるアイテムが含まれています。
exl-id: 3ede15d4-4c39-442a-8784-2d5e6650fe67
feature: Products
role: Developer
source-git-commit: d51fd4d7b064b8eea6cd3771af279b74a8bdec48
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Adobe Commerce 2.3.5 の一括アクション製品数の既知の問題

ここでは、Adobe Commerce 2.3.5 の既知の問題について説明します。管理画面での一括アクションの後にマーチャントが受け取る通知に、誤った数の影響を受けるアイテムが含まれています。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.3.5 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.3.5

## 問題

一括操作（製品の一括更新や読み込み/書き出しなど）の後にAdobe Commerceが表示するシステムメッセージには、一括操作の影響を受ける製品の正確な数ではなく、数が 0 と表示されます。

## 修正

修正は、2020 年 Q4 にリリースされるAdobe Commerce 2.3.6 で利用できるようになります。

## 関連資料

* Adobe Commerce 2.3.5 の既知の問題に関するAdobe Commerce サポートナレッジベースの記事：
   * [Adobe Commerce 2.3.5 でバーチャル商品が正しく処理されない複数出荷の注文](/help/troubleshooting/miscellaneous/magento-2-3-5-known-issue-virtual-product-multi-ship-orders.md)
   * [Adobe Commerce 2.3.5 の製品比較の既知の問題](/help/troubleshooting/storefront/product-comparison-known-issue-in-magento-2-3-5.md)
   * [Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.5 および 2.3.5-p1 における国の支払い方法の問題](/help/troubleshooting/known-issues-patches-attached/magento-2-3-5-2-3-5-p1-patch-country-payment-issue.md)
   * [Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ](/help/troubleshooting/payments/patch-for-amazon-pay-checkout-issue-in-magento-2-3-5-p1.md)
   * [Adobe Commerce 2.3.5 の既知の問題については、開発者向けドキュメントを参照してください ](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#known-issues)
