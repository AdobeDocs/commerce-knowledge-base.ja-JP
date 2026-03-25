---
title: Adobe Commerce 2.4.0 Braintree Virtual Terminal ページが破損しています
description: この記事では、Adobe Commerce 2.4.0の既知の問題に対するパッチを提供します。このパッチでは、Braintree Virtual Terminal ページで適切なUI要素が読み込まれない、またはBraintreeが設定されていない場合に適切なエラーメッセージが表示されない場合があります。
exl-id: 1d4d762d-2ab3-4752-ad6d-1eb6a179917d
feature: Orders, Payments
role: Developer
source-git-commit: 1dcd003bd9b08741c0fba464f5520797cfaeccbb
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 Braintree Virtual Terminal ページが破損しています

この記事では、Adobe Commerce 2.4.0の既知の問題に対するパッチを提供します。このパッチでは、Braintree Virtual Terminal ページで適切なUI要素が読み込まれない、またはBraintreeが設定されていない場合に適切なエラーメッセージが表示されない場合があります。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* Adobe Commerce on cloud infrastructure 2.4.0

## イシュー

### シナリオ 1: Braintreeの支払い方法が設定されている

<u>再生する手順：</u>

Commerce Adminで、**Sales** > **Braintree Virtual Terminal**&#x200B;に移動します。** **

<u>期待される結果：</u>

**Braintree Virtual Terminal** ページが適切なUIで読み込まれます。

<u>実際の結果：</u>

**Braintree Virtual Terminal** ページのUIが壊れています。

### シナリオ 2: Braintreeの支払い方法が設定されている

<u>再生する手順：</u>

Commerce Adminで、**Sales** > **Braintree Virtual Terminal**&#x200B;に移動します。** **

<u>期待される結果：</u>

**Braintree Virtual Terminal** ページが適切なUIで読み込まれ、Braintreeがまだ設定されていないことを知らせる警告が表示されます。

<u>実際の結果：</u>

**Braintree Virtual Terminal** ページのUIが壊れ、警告は表示されません。

## Solution

この記事に記載されているパッチを適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後までスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[BUNDLE-2670-composer.patch](assets/BUNDLE-2670-composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次の目的で作成されました。

* Adobe Commerce on cloud infrastructure 2.4.0
* Adobe Commerce オンプレミス 2.4.0

## パッチの適用方法

手順については、[Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/how-to-apply-a-composer-patch-provided-by-magento)が提供するコンポーザーパッチの適用方法を参照してください。

## 添付ファイル
