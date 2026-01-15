---
title: Adobe Commerce 2.4.0:B2B 1.2.0 インストール中の例外
description: この記事では、B2B 1.2.0 のインストール時に「setup:upgrade」の際にスローされる例外に対する、Adobe Commerceの既知の問題を修正しました。
exl-id: 2c1dadd9-7754-4b4c-8d37-b75c13beae5c
feature: B2B, Install, Upgrade
role: Developer
source-git-commit: 05297c82b292b8ccc88018c58e991bd3a32d6ffa
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:B2B 1.2.0 インストール中の例外

この記事では、B2B 1.2.0 のインストール時に `setup:upgrade` 中にスローされる例外に対するAdobe Commerceの既知の問題を修正しました。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* B2B 1.2.0

## 問題

<u> 再現手順 </u>

1. 複数のストアが作成されたAdobe Commerceをインストールします。
1. 追加のストアを作成します。
1. B2B 1.2.0 のインストール

>[!WARNING]
>
>1.2.0 未満のバージョンまたは 2.4.0 未満のCommerce インスタンスから 1 つ以上のストアを含む B2B インスタンスのアップグレードも影響を受けます。

<u> 期待される結果 </u>

B2B 1.2.0 のインストール。

<u> 実際の結果 </u>

`setup:upgrade` を実行して B2B 1.2.0 をインストールすると、`PurchaseOrder` モジュールに次のエラーが表示されます。

```php
Module 'Magento_PurchaseOrder':
  Unable to apply data patch Magento\PurchaseOrder\Setup\Patch\Data\InitPurchaseOrderSalesSequence
  for module Magento_PurchaseOrder. Original exception message: DDL statements
  are not allowed in transactions
```

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

パッチはこの記事に添付されており、（ファイルを解凍した後に） `.composer` 形式と `.git` 形式の両方でダウンロードできます。

ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のいずれかのリンクをクリックします。

* [Composer パッチ B2B-716\_composer.patch](assets/B2B-716_composer.patch.zip)
* [Git パッチ B2B-716\_git.patch](assets/B2B-716_git.patch.zip)

## パッチの適用方法

<u>Composer パッチ </u>

Composer パッチの手順については、[Adobeが提供する Composer パッチの適用方法 &#x200B;](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

<u>Git パッチ </u>

* クラウドインフラストラクチャー上のAdobe Commerceに対する Git パッチの手順については、開発者向けドキュメントの [&#x200B; パッチを適用する &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches) を参照してください。
* Adobe Commerceの Git パッチ手順については、開発者向けドキュメントの [&#x200B; パッチの適用：カスタムパッチ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/patches/overview#custom-patches) を参照してください。

## 関連資料

* [Adobe Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintreeの支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 既知の問題：チェックアウト時に一部の国でローカル支払い方法を選択中にエラーメッセージが表示される](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
* [Adobe Commerce 2.4.0 B2B 管理者が、設定可能な商品を見積もりに追加できない](/help/troubleshooting/miscellaneous/magento-2-4-0-b2b-admin-can-t-add-configurable-product-to-quote.md)
