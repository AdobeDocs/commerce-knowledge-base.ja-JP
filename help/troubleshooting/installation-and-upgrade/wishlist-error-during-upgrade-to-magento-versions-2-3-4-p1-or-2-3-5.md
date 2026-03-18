---
title: Adobe Commerce バージョン 2.3.4-p1 または 2.3.5 へのアップグレード中のウィッシュリストエラー
description: ここでは、Adobe Commerce バージョン 2.3.4-p1 および 2.3.5 へのアップグレード時のウィッシュリストエラーに関連する既知の問題について説明します。
exl-id: 97479615-bf3f-4544-a9c1-8f19ba74318e
feature: Install, Upgrade
role: Developer
source-git-commit: 8be0c125bb0417e34e016656337506da88796630
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Adobe Commerce バージョン 2.3.4-p1 または 2.3.5 へのアップグレード中のウィッシュリストエラー

ここでは、Adobe Commerce バージョン 2.3.4-p1 および 2.3.5 へのアップグレード時のウィッシュリストエラーに関連する既知の問題について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.4-p1 および 2.3.5
* Adobe Commerce オンプレミス 2.3.4-p1 および 2.3.5

## 問題

Adobe Commerce（すべてのデプロイメント方法）およびMagento Open Sourceをバージョン 2.3.5 または 2.3.4-p1 にアップグレードすると、モジュールからウィッシュリストエラー（以下で詳しく説明）が発生する場合があります。

```php
Magento_Wishlist
```

Adobe Commerce（すべてのデプロイメント方法）/Magneto Open Source version 2.3.4-p1 **version 2.3.4-p2 に** またはAdobe Commerce（すべてのデプロイメント方法）/Magneto Open Source version 2.3.5 **version 2.3.5-p1** からアップグレードすると、エラーが修正されます。

<u> 再現手順 </u>:

Adobe Commerce（すべてのデプロイメント方法）/Magento Open Sourceをバージョン 2.3.4-p1 または 2.3.5 にアップグレードします。

<u> 期待される結果 </u>:

Adobe Commerce（すべてのデプロイメント方法）/Magento Open Source バージョン 2.3.4-p1 または 2.3.5 へのアップグレードプロセスは通常どおり完了します。

<u> 実際の結果 </u>:

アップグレード中に、次のエラーが発生します。

```php
Module ‘Magento_Wishlist’:

Unable to apply data patch Magento\Wishlist\Setup\Patch\Data\CleanUpData for module Magento_Wishlist. Original exception message: Unable to unserialize value. Error: Syntax error
```

## 解決策

* Adobe Commerce（すべてのデプロイメント方法）/Magneto Open Source バージョン 2.3.5 にアップグレードする場合は、**バージョン 2.3.5-p1 にアップグレード** してください。 Adobe Commerce（すべてのデプロイメント方法）/Magento Open Source バージョン 2.3.5-p1 は 2.3.5 に代わるものです。
* Adobe Commerce（すべてのデプロイメント方法）/Magento Open Source バージョン 2.3.4-p1 にアップグレードしていた場合は、**バージョン 2.3.4-p2 にアップグレード** してください。 Adobe Commerce（すべての導入方法）/Magneto Open Source 2.3.4-p2 は 2.3.4-p1 に代わるものです。

## 関連資料

開発者向けドキュメントでは、

* [&#x200B; クラウドインフラストラクチャー上のAdobe Commerceガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/overview)
* [&#x200B; クラウドインフラストラクチャー上のAdobe Commerce - Adobe Commerceのバージョンをアップグレード &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version)
* [Adobe Commerce オンプレミスおよびAdobe Commerce - Magento Open Source アプリケーションおよびモジュールをアップグレードし &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/overview) す。
* [&#x200B; ウィッシュリスト項目の設定ページ &#x200B;](https://developer.adobe.com/commerce/frontend-core/guide/layouts/product-layouts#wishlist-item-configure-page)
* [&#x200B; 高度なレポートを提供するモジュール &#x200B;](https://developer.adobe.com/commerce/php/development/advanced-reporting/modules/)
