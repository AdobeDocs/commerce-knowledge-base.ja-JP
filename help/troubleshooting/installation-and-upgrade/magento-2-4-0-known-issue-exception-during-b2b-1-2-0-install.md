---
title: Adobe Commerce 2.4.0:B2B 1.2.0 インストール時の例外
description: この記事では、B2B 1.2.0のインストール時に「setup:upgrade」中に発生する例外に関するAdobe Commerceの既知の問題の修正点を紹介します。
exl-id: 2c1dadd9-7754-4b4c-8d37-b75c13beae5c
feature: B2B, Install, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
subfeature_v2:
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '334'
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

Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)が提供するコンポーザーのパッチの適用方法については、[ コンポーザーのパッチの適用方法を参照してください。

<u>Git パッチ </u>

* クラウドインフラストラクチャ上のAdobe CommerceのGit パッチ手順については、開発者向けドキュメントの「[ パッチを適用](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)」を参照してください。
* Adobe CommerceのGit パッチの手順については、開発者向けドキュメントの「[ パッチの適用：カスタムパッチ ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/patches/overview#custom-patches)」を参照してください。

## 関連トピックス

* [Adobe Commerce 2.4.0の既知の問題：Braintreeの支払い方法が複数のアドレスのチェックアウトに表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0の既知の問題：一部の国でチェックアウト時に表示される「ローカル支払い方法を選択する」というエラーメッセージ](/help/troubleshooting/payments/magento-2-4-0-checkout-error-selecting-local-payments.md)
