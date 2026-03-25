---
title: Adobe Commerce 2.4.0:B2B 1.2.0 インストール時の例外
description: この記事では、B2B 1.2.0のインストール時に「setup:upgrade」中に発生する例外に関するAdobe Commerceの既知の問題の修正点を紹介します。
exl-id: 2c1dadd9-7754-4b4c-8d37-b75c13beae5c
feature: B2B, Install, Upgrade
role: Developer
source-git-commit: 1dcd003bd9b08741c0fba464f5520797cfaeccbb
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Adobe Commerce 2.4.0:B2B 1.2.0 インストール時の例外

この記事では、B2B 1.2.0のインストール時に`setup:upgrade`中にスローされた例外に関するAdobe Commerceの既知の問題の修正について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* Adobe Commerce on cloud infrastructure 2.4.0
* B2B 1.2.0

## イシュー

<u>複製する手順</u>

1. 複数のストアを作成してAdobe Commerceをインストールします。
1. 追加のストアを作成します。
1. B2B 1.2.0をインストールします。

>[!WARNING]
>
>また、バージョン 1.2.0未満またはCommerce インスタンス 2.4.0未満のバージョンから1つ以上のストアを持つB2B インスタンスのアップグレードも影響を受けます。

<u>期待される結果</u>

B2B 1.2.0のインストール。

<u>実際の結果</u>

`setup:upgrade`がB2B 1.2.0のインストールを実行すると、このエラーが`PurchaseOrder` モジュールに表示されます。

```php
Module 'Magento_PurchaseOrder':
  Unable to apply data patch Magento\PurchaseOrder\Setup\Patch\Data\InitPurchaseOrderSalesSequence
  for module Magento_PurchaseOrder. Original exception message: DDL statements
  are not allowed in transactions
```

## Solution

この記事に記載されているパッチを適用します。

## パッチ

この記事にパッチが添付されており、`.composer`と`.git`の両方の形式でダウンロードできます（ファイルを解凍した後）。

ダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のいずれかのリンクをクリックします。

* [Composer パッチ B2B-716\_composer.patch](assets/B2B-716_composer.patch.zip)
* [Git パッチ B2B-716\_git.patch](assets/B2B-716_git.patch.zip)

## パッチの適用方法

<u> コンポーザーのパッチ </u>

Adobe[が提供するコンポーザーのパッチの適用方法については、](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento) コンポーザーのパッチの適用方法を参照してください。

<u>Git パッチ </u>

* クラウドインフラストラクチャ上のAdobe CommerceのGit パッチ手順については、開発者向けドキュメントの「[&#x200B; パッチを適用](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)」を参照してください。
* Adobe CommerceのGit パッチの手順については、開発者向けドキュメントの「[&#x200B; パッチの適用：カスタムパッチ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/patches/overview#custom-patches)」を参照してください。

## 関連トピックス

* [Adobe Commerce 2.4.0の既知の問題：Braintreeの支払い方法が複数のアドレスのチェックアウトに表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0の既知の問題：一部の国でチェックアウト時に表示される「ローカル支払い方法を選択する」というエラーメッセージ](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
