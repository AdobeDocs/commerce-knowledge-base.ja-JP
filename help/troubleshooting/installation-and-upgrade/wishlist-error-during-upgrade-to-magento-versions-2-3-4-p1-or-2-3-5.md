---
title: Adobe Commerce バージョン 2.3.4-p1または2.3.5へのアップグレード時のWishlist エラー
description: この記事では、Adobe Commerce バージョン 2.3.4-p1および2.3.5にアップグレードする際に、これらのバージョンへのアップグレード中に発生するwishlist エラーに関連する既知の問題に対する修正を提供します。
exl-id: 97479615-bf3f-4544-a9c1-8f19ba74318e
feature: Install, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%
---
# Adobe Commerce バージョン 2.3.4-p1または2.3.5へのアップグレード時のWishlist エラー

この記事では、Adobe Commerce バージョン 2.3.4-p1および2.3.5にアップグレードする際に、これらのバージョンへのアップグレード中に発生するwishlist エラーに関連する既知の問題に対する修正を提供します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.3.4-p1および2.3.5
* Adobe Commerce オンプレミス 2.3.4-p1および2.3.5

## イシュー

Adobe Commerce（すべてのデプロイメント方式）とMagento Open Sourceをバージョン 2.3.5または2.3.4-p1にアップグレードすると、モジュールからウィッシュリストエラー（詳細は以下を参照）が発生する可能性があります。

```php
Magento_Wishlist
```

Adobe Commerce（すべてのデプロイメント方式）/Magneto Open Source バージョン 2.3.4-p1 **からバージョン 2.3.4-p2**&#x200B;またはAdobe Commerce（すべてのデプロイメント方式）/Magneto Open Source バージョン 2.3.5 **からバージョン 2.3.5-p1**&#x200B;にアップグレードすると、エラーが修正されます。

<u>複製する手順</u>:

Adobe Commerce（すべてのデプロイメント方法）/Magento Open Sourceをバージョン 2.3.4-p1または2.3.5にアップグレードします。

<u>期待される結果</u>:

Adobe Commerce（すべてのデプロイメント方法）/Magento Open Source バージョン 2.3.4-p1または2.3.5へのアップグレードプロセスは正常に完了します。

<u>実際の結果</u>:

アップグレード中に、次のエラーが発生します。

```php
Module ‘Magento_Wishlist’:

Unable to apply data patch Magento\Wishlist\Setup\Patch\Data\CleanUpData for module Magento_Wishlist. Original exception message: Unable to unserialize value. Error: Syntax error
```

## 解決策

* Adobe Commerce（すべてのデプロイメント方式）/Magneto Open Source バージョン 2.3.5にアップグレードする場合は、**バージョン 2.3.5-p1**&#x200B;にアップグレードします。 Adobe Commerce（すべてのデプロイメント方法）/Magento Open Source バージョン 2.3.5-p1は、2.3.5に代わるものです。
* Adobe Commerce（すべてのデプロイメント方式）/Magento Open Source バージョン 2.3.4-p1にアップグレードする場合は、**バージョン 2.3.4-p2**&#x200B;にアップグレードします。 Adobe Commerce（すべてのデプロイメント方法）/Magneto Open Source バージョン 2.3.4-p2は、バージョン 2.3.4-p1に代わるものです。

## 関連トピックス

アドビの開発者ドキュメントには、次のようなものがあります。

* [Adobe Commerce オンクラウド基盤ガイド](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/overview)
* [Adobe Commerce on cloud infrastructure - Adobe Commerce バージョンのアップグレード](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version)
* [Adobe Commerce オンプレミスおよびMagento Open Source - Adobe Commerce アプリケーションとモジュールのアップグレード](https://experienceleague.adobe.com/ja/docs/commerce-operations/upgrade-guide/overview)
* [ウィッシュリスト項目設定ページ](https://developer.adobe.com/commerce/frontend-core/guide/layouts/product-layouts#wishlist-item-configure-page)
* [高度なレポートを提供するモジュール](https://developer.adobe.com/commerce/php/development/advanced-reporting/modules/)
