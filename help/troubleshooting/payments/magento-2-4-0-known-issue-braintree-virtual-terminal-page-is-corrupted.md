---
title: Adobe Commerce 2.4.0Braintreeのバーチャルターミナルページが破損する
description: この記事では、Adobe Commerce 2.4.0 の既知の問題に対するパッチを提供します。このパッチでは、Braintreeバーチャルターミナルページが適切な UI 要素を読み込まず、Braintreeが設定されていない場合は適切なエラーメッセージが表示されません。
exl-id: 1d4d762d-2ab3-4752-ad6d-1eb6a179917d
feature: Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Adobe Commerce 2.4.0Braintreeのバーチャルターミナルページが破損する

この記事では、Adobe Commerce 2.4.0 の既知の問題に対するパッチを提供します。このパッチでは、Braintreeバーチャルターミナルページが適切な UI 要素を読み込まず、Braintreeが設定されていない場合は適切なエラーメッセージが表示されません。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

## 問題

### シナリオ 1:Braintree支払方法が構成される

<u>再現手順：</u>

Commerce Admin で、に移動します。 **売上** > **Braintreeバーチャル端末** .** **

<u>期待される結果：</u>

この **Braintreeバーチャル端末** 適切な UI でページが読み込まれます。

<u>実際の結果：</u>

の UI **Braintreeバーチャル端末** ページが破損している。

### シナリオ 2:Braintree支払方法が設定される

<u>再現手順：</u>

Commerce Admin で、に移動します。 **売上** > **Braintreeバーチャル端末** .** **

<u>期待される結果：</u>

この **Braintreeバーチャル端末** 適切な UI でページが読み込まれ、Braintreeがまだ設定されていないことを示す警告が表示されます。

<u>実際の結果：</u>

の UI **Braintreeバーチャル端末** ページが破損しており、警告は表示されません。

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[BUNDLE-2670-composer.patch](assets/BUNDLE-2670-composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0

## パッチの適用方法

参照： [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) 説明を参照してください。

## 添付ファイル
