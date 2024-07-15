---
title: 「Adobe Commerce 2.4.0 パッチ：配送ラベル作成の問題を返す」
description: この記事では、お客様の返品用の配送ラベルの印刷で問題が発生した場合の、Adobe Commerce 2.4.0 の既知の問題に対するパッチを提供します。
exl-id: f78f8d7e-29e9-4d6c-83f6-cd5afa1d7d9c
feature: B2B, Orders, Returns, Communications, Shipping/Delivery
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 パッチ：配送ラベル作成の問題が返される

この記事では、お客様の返品用の配送ラベルの印刷で問題が発生した場合の、Adobe Commerce 2.4.0 の既知の問題に対するパッチを提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## 問題

<u> 再現手順：</u>

1. FedEx、DHL、UPS、USPS のいずれかの主要な配送方法を使用して注文を行い、注文を完了します。
1. この注文の返品を作成して承認します。
1. 承認済みの **返品情報** ページを開き、「**配送ラベルを作成**」ボタンをクリックします。
1. 発送方法を選択し、商品をパッケージに追加して、「保存」をクリックします。

<u> 期待される結果：</u>

配送ラベルが正常に作成され、「*配送ラベルが作成されました。* というメッセージが表示されます。

<u> 実際の結果：</u>

**返品情報** ページが破損しており、「返品情報」ページに次のエラーメッセージが表示されます。*一般情報このセクションには、保存されていない変更が加えられました。 このタブには無効なデータが含まれています*。

## 解決策

この記事で提供されている [ パッチ ](assets/MC-35984-2.4.0-CE-composer.patch.zip) を適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MC-35984-2.4.0-CE-composer.patch](assets/MC-35984-2.4.0-CE-composer.patch.zip)

このパッチは、`.git` と `.composer` の両方の形式で、[Adobe Commerce ダウンロード ](https://magento.com/tech-resources/download) ページの左側の列のナビゲーションにある **パッチ** からもダウンロードできます。 MC-35984 パッチを検索します。

## パッチの適用方法

手順については、サポートナレッジページの [Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## サポートナレッジベースの関連するリーディング：

* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
* [Adobe Commerce 2.4.0 での配送ラベル作成の既知の問題](/help/troubleshooting/known-issues-patches-attached/shipping-labels-creation-known-issue-in-magento-2-4-0.md)
