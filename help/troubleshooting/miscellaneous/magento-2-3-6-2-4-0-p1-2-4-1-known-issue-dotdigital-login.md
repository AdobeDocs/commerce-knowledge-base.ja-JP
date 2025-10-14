---
title: 'Adobe Commerce 2.3.6、2.4.0-p1、2.4.1 既知の問題：dotdigital login'
description: ここでは、dotdigital アカウントが有効な場合に、管理パネルから [dotdigital] （https://dotdigital.com/）にログインできないAdobe Commerce 2.3.6、2.4.0-p1、および 2.4.1 の既知の問題について説明します。
exl-id: 427d895c-8c03-4ced-813a-eeaa67f1d1f0
feature: Configuration
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Adobe Commerce 2.3.6、2.4.0-p1、2.4.1 既知の問題：dotdigital login

ここでは、dotdigital アカウントが有効な場合に、管理パネルから [dotdigital](https://dotdigital.com/) にログインできない、Adobe Commerce 2.3.6、2.4.0-p1、および 2.4.1 の既知の問題について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.6 （Safari ブラウザーのみ）
* Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.4.0-p1 （Safari ブラウザーのみ）
* Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.4.1 （Safari ブラウザーのみ）

## 問題

<u> 前提条件 </u>:

1. dotdigital アカウントが存在します。
1. Adobe Commerceには、有効な dotdigital API 資格情報が存在します。

<u> 再現手順 </u>:

1. **ストア**/**設定**/**DOTDIGITAL**/**チャット設定**/**有効** が *はい* に設定されていることを確認します。
1. **チャットウィジェットを設定** または **チャットチームを設定** の **設定** をクリックします。

<u> 期待される結果 </u>:

管理パネルを使用してチャット設定ページが正常に開きます。

<u> 実際の結果 </u>:

dotdigital にログインできません。

## 解決策

回避策：この特定の状況では、Safari の代替ブラウザーを使用します。

## 関連資料

[Adobe Commerce 2.4.1 既知の問題 – Vertex アドレスが別の配送先/請求先アドレスで検証されない問題 &#x200B;](/help/troubleshooting/miscellaneous/magento-2-4-1-vertex-address-validation-message-post-address-update.md) アドビのサポートナレッジベースにあります。
