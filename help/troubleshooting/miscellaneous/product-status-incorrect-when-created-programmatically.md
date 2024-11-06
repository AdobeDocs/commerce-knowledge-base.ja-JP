---
title: プログラムで作成した場合に、製品ステータスが不正確になる
description: この記事では、プログラムによって作成または更新された際に、製品ステータスが無効で、製品がストアフロントに表示されない場合や、間違ったストアビューに割り当てられる場合の修正について説明します。
exl-id: ac02f961-f9e2-4620-839f-b8dbd0befb15
feature: Products
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# プログラムで作成した場合に、製品ステータスが不正確になる

この記事では、プログラムによって作成または更新された際に、製品ステータスが無効で、製品がストアフロントに表示されない場合や、間違ったストアビューに割り当てられる場合の修正について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.X.X

## 問題

Adobe Commerce アプリケーションがブートストラップされたスクリプトから、カタログ商品がプログラムで作成または更新されると、商品のステータスが無効になったり、間違ったストアビューに割り当てられたりする可能性があります。

## 原因：

この問題は、Adobe Commerce インスタンスの管理者ロールに ACL 制限が設定されているために発生する場合があります。 ブートストラップされたアプリケーションの場合、適切な ACL 設定を持つ初期化された管理セッションはありません。 その場合、`Magento_AdminGws` モジュールで検証が失敗します。これは、そのようなアクションに対する権限チェックを担当します。

## 製品ステータスが正しくない場合の解決策

開発者向けドキュメントの [ObjectManager> プログラムによる製品アップデート ](https://developer.adobe.com/commerce/php/development/components/object-manager/) トピックで説明しているように、`Magento\Framework\Authorization\PolicyInterface` ーザーの動的 DI 環境設定を設定します。

## 関連資料

* [Github:productRepository で作成された製品のステータスを変更できない ](https://github.com/magento/magento2/issues/5664)
