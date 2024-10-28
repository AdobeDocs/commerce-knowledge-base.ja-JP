---
title: 「Adobe Commerce 2.3.5 の既知の問題：バーチャル製品の複数出荷注文」
description: ここでは、バーチャル商品を含む複数配送の注文が正しく処理されない、Adobe Commerce 2.3.5 の既知の問題について説明します。
exl-id: 34ce79a2-5157-492b-8ee4-bdc09aae0c40
feature: Orders, Products, Shipping/Delivery
role: Developer
source-git-commit: d51fd4d7b064b8eea6cd3771af279b74a8bdec48
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Adobe Commerce 2.3.5 の既知の問題：バーチャル製品の複数出荷注文

ここでは、バーチャル商品を含む複数配送の注文が正しく処理されない、Adobe Commerce 2.3.5 の既知の問題について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.5
* クラウドインフラストラクチャー 2.3.5 上のAdobe Commerce

## 問題

<u> 再現手順 </u>:

1. ストアフロントで、物理的な製品と仮想製品を買い物かごに追加します。
1. チェックアウトに進み、「**複数のアドレスを使用してチェックアウト**」を選択します。
1. 必要な情報をすべて追加して注文します。

<u> 期待される結果 </u>:

すべての製品の注文が正常に行われます。

<u> 実際の結果 </u>:

仮想製品の順序が空です。

## 修正

修正は、2020 年 Q4 にリリースされるAdobe Commerce 2.3.6 で利用できるようになります。

## 関連資料

サポートナレッジベースでは、

* [Adobe Commerce 2.3.5 の製品比較の既知の問題](/help/troubleshooting/storefront/product-comparison-known-issue-in-magento-2-3-5.md)
* [Adobe Commerce 2.3.5 の一括アクション製品数の既知の問題](/help/troubleshooting/miscellaneous/bulk-action-product-count-known-issue-in-magento-2-3-5.md)
* [Adobe Commerce 2.3.5 および 2.3.5-p1 における国別の支払方法の問題](/help/troubleshooting/known-issues-patches-attached/magento-2-3-5-2-3-5-p1-patch-country-payment-issue.md)
* [Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ](/help/troubleshooting/payments/patch-for-amazon-pay-checkout-issue-in-magento-2-3-5-p1.md)

開発者向けドキュメントでは、

* [Adobe Commerce 2.3.5 リリースノート ](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#known-issues)
