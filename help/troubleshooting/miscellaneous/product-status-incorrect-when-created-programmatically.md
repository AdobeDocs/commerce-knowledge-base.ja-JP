---
title: プログラムで作成した製品ステータスが正しくない
description: この記事では、プログラムで製品ステータスが「無効」になり、製品がストアフロントに表示されない場合、または誤ったストアビューに割り当てられる場合の修正について説明します。
exl-id: ac02f961-f9e2-4620-839f-b8dbd0befb15
feature: Products
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%
---
# プログラムで作成した製品ステータスが正しくない

この記事では、プログラムで製品ステータスが「無効」になり、製品がストアフロントに表示されない場合、または誤ったストアビューに割り当てられる場合の修正について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure 2.X.X
* Adobe Commerce オンプレミス 2.X.X

## イシュー

Adobe Commerce アプリケーションがブートストラップされたスクリプトからカタログ製品がプログラムで作成または更新されると、製品のステータスが「無効」になったり、間違ったストアビューに割り当てられたりする可能性があります。

## 原因

この問題は、Adobe Commerce インスタンス管理者ロールに設定されたACL制限が原因で発生する場合があります。 ブートストラップされたアプリケーションの場合、適切なACL設定を持つ初期化された管理者セッションはありません。 これにより、このようなアクションの権限チェックを担当する`Magento_AdminGws` モジュールで検証が失敗します。

## 誤った製品ステータスの解決策

開発者ドキュメントの[ObjectManager> プログラマティック製品アップデート ](https://developer.adobe.com/commerce/php/development/components/object-manager/) トピックで説明されているように、`Magento\Framework\Authorization\PolicyInterface`の動的DI環境設定を設定します。

## 関連トピックス

* [Github:productRepositoryで作成した製品のステータスを変更できない](https://github.com/magento/magento2/issues/5664)
