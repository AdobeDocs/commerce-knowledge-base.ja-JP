---
title: Adobe Commerce バージョン 2.3.4-p1 または 2.3.5 へのアップグレード中のウィッシュリストエラー
description: ここでは、Adobe Commerce バージョン 2.3.4-p1 および 2.3.5 へのアップグレード時のウィッシュリストエラーに関連する既知の問題について説明します。
exl-id: 97479615-bf3f-4544-a9c1-8f19ba74318e
feature: Install, Upgrade
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
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

Adobe Commerce（すべてのデプロイメント方法）をアップグレードし、Magento Open Sourceを 2.3.5 または 2.3.4-p1 に移行すると、モジュールからウィッシュリストエラー（以下で詳しく説明）が発生する場合があります。

```php
Magento_Wishlist
```

Adobe Commerce（すべてのデプロイメント方法）/Magneto Open Source version 2.3.4-p1 **version 2.3.4-p2 に** またはAdobe Commerce（すべてのデプロイメント方法）/Magneto Open Source version 2.3.5 **version 2.3.5-p1** からアップグレードすると、エラーが修正されます。

<u> 再現手順 </u>:

Adobe Commerce（すべてのデプロイメント方法）/Magento Open Sourceをバージョン 2.3.4-p1 または 2.3.5 にアップグレードします。

<u> 期待される結果 </u>:

Adobe Commerce（すべてのデプロイメント方法）/Magento Open Sourceバージョン 2.3.4-p1 または 2.3.5 へのアップグレードプロセスは通常どおり完了します。

<u> 実際の結果 </u>:

アップグレード中に、次のエラーが発生します。

```php
Module ‘Magento_Wishlist’:

Unable to apply data patch Magento\Wishlist\Setup\Patch\Data\CleanUpData for module Magento_Wishlist. Original exception message: Unable to unserialize value. Error: Syntax error
```

## 解決策

* Adobe Commerce（すべてのデプロイメント方法）/Magneto Open Source バージョン 2.3.5 にアップグレードする場合は、**バージョン 2.3.5-p1 にアップグレード** してください。 Adobe Commerce（すべてのデプロイメント方法）/Magento Open Sourceバージョン 2.3.5-p1 は 2.3.5 に代わるものです。
* Adobe Commerce（すべてのデプロイメント方法）/Magento Open Sourceバージョン 2.3.4-p1 にアップグレードしていた場合は、**バージョン 2.3.4-p2 にアップグレード** してください。 Adobe Commerce（すべての導入方法）/Magneto Open Source 2.3.4-p2 は 2.3.4-p1 に代わるものです。

## 関連資料

開発者向けドキュメントでは、

* [ クラウドインフラストラクチャー上のAdobe Commerceガイド ](https://devdocs.magento.com/cloud/bk-cloud.html)
* [ クラウドインフラストラクチャー上のAdobe Commerce - Adobe Commerceのバージョンをアップグレード ](https://devdocs.magento.com/cloud/project/project-upgrade.html)
* [Adobe Commerceのオンプレミスおよびモジュール - Adobe Commerce Magento Open Sourceとモジュールをアップグレードし ](https://devdocs.magento.com/guides/v2.3/comp-mgr/bk-compman-upgrade-guide.html) す。
* [ ウィッシュリスト項目の設定ページ ](https://devdocs.magento.com/guides/v2.3/frontend-dev-guide/layouts/product-layouts.html#wishlist-item-configure-page)
* [ 高度なレポートを提供するモジュール ](https://devdocs.magento.com/guides/v2.3/advanced-reporting/modules.html)
