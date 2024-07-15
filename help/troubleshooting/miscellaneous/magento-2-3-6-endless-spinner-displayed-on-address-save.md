---
title: 「Adobe Commerce 2.3.6：アドレス保存時に表示される無限のスピナー」
description: この記事では、Adobe Commerce 2.3.6 でストアフロントの「マイアカウント」にアドレスを保存すると、待機中のスピナーが無期限に表示される既知の問題について説明します。
exl-id: 63841114-167e-4915-b6ed-ee0ef4eae36e
feature: Shipping/Delivery, Orders, Checkout
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Adobe Commerce 2.3.6：アドレス保存時に表示されるエンドレススピナー

この記事では、Adobe Commerce 2.3.6 でストアフロントの「マイアカウント」にアドレスを保存すると、待機中のスピナーが無期限に表示される既知の問題について説明します。

## 影響を受ける製品とバージョン

* Vertex 統合が有効なAdobe Commerce 2.3.6 （Firefox ブラウザーのみ）

## 問題

ストアフロントの「自分のアカウント」セクションにアドレスを保存すると、Vertex Core JS のエラーが原因で、待機中のスピナーが無期限に表示されることがあります。

## 回避策

回避策：Firefox の代替ブラウザーを使用します。

この問題は、Adobe Commerce 2.3.1 で修正されました。

## 関連資料

* サポートナレッジベースで [VertexAddress クレンジングを使用して「請求先と配送先住所が同じです」を選択解除する場合、異なる住所は使用できません ](/help/troubleshooting/miscellaneous/vertex-address-cleansing-different-addresses-not-allowed.md)。
* [Adobe Commerce 2.4.1 Vertex Address validation message post address update](/help/troubleshooting/miscellaneous/magento-2-4-1-vertex-address-validation-message-post-address-update.md) （サポートナレッジベース）。
