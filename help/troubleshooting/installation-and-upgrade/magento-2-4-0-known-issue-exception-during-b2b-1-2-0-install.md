---
title: 「Adobe Commerce 2.4.0:B2B 1.2.0 インストール中の例外」
description: この記事では、B2B 1.2.0 のインストール時に「setup:upgrade」の際にスローされる例外に対する、Adobe Commerceの既知の問題を修正しました。
exl-id: 2c1dadd9-7754-4b4c-8d37-b75c13beae5c
feature: B2B, Install, Upgrade
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:B2B 1.2.0 インストール中の例外

この記事では、次の期間にスローされた例外に関するAdobe Commerceの既知の問題を修正します `setup:upgrade` b2B 1.2.0 をインストールする場合。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* B2B 1.2.0

## 問題

<u>再現手順</u>

1. 複数のストアが作成されたAdobe Commerceをインストールします。
1. 追加のストアを作成します。
1. B2B 1.2.0 のインストール

>[!WARNING]
>
>1.2.0 未満のバージョンまたは 2.4.0 未満のCommerce インスタンスから 1 つ以上のストアを含む B2B インスタンスのアップグレードも影響を受けます。

<u>期待される結果</u>

B2B 1.2.0 のインストール。

<u>実際の結果</u>

条件 `setup:upgrade` b2B 1.2.0 をインストールするために実行します。このエラーは、 `PurchaseOrder` モジュール：

```php
Module 'Magento_PurchaseOrder':
  Unable to apply data patch Magento\PurchaseOrder\Setup\Patch\Data\InitPurchaseOrderSalesSequence
  for module Magento_PurchaseOrder. Original exception message: DDL statements
  are not allowed in transactions
```

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

パッチはこの記事に添付されており、両方からダウンロードできます `.composer` および `.git` 形式（ファイルを解凍した後）。

ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のいずれかのリンクをクリックします。

* [Composer パッチ B2B-716\_composer.patch](assets/B2B-716_composer.patch.zip)
* [Git パッチ B2B-716\_git.patch](assets/B2B-716_git.patch.zip)

## パッチの適用方法

<u>Composer パッチ </u>

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) （composer のパッチ手順）

<u>Git パッチ </u>

* 参照： [パッチの適用](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントの git に関する cloud infrastructure 上のAdobe Commerceのパッチ手順。
* 参照： [パッチの適用：カスタム パッチ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#custom-patches) 開発者向けドキュメントの git に関するAdobe Commerceのパッチ手順。

## 関連資料

* [Adobe Commerce 2.4.0 の既知の問題：ストアフロントに生のメッセージデータが表示される](/help/troubleshooting/storefront/magento-2-4-0-issue-storefront-raw-message-data-display.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 の既知の問題：複数配送のチェックアウトで報酬ポイントを削除する際に 404 エラーが発生する](/help/troubleshooting/storefront/magento-2-4-0-404-error-removing-rewards-points-on-multi-shipping-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：注文の表示エラー](/help/troubleshooting/storefront/magento-2-4-0-known-issue-orders-display-error.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
* [Adobe Commerce 2.4.0 での配送ラベル作成の既知の問題](/help/troubleshooting/known-issues-patches-attached/shipping-labels-creation-known-issue-in-magento-2-4-0.md)
* [Adobe Commerce 2.4.0 の既知の問題 – 顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
