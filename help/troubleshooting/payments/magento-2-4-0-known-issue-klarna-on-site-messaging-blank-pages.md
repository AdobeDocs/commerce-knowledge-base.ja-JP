---
title: Adobe Commerce 2.4.0既知の問題：Klarna オンサイトメッセージングの空白ページ
description: ここでは、Klarnaの支払い方法に関する既知のAdobe Commerce 2.4.0の問題について説明します。この問題では、デザインテーマを指定せずにKlarnaのオンサイトメッセージを有効にすると、ストアフロントに商品ページが正しく表示されません（商品ページが空白で表示されます）。
exl-id: f0f9edfc-eaad-4947-9200-41e217bfbe84
feature: Orders, Payments
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%
---
# Adobe Commerce 2.4.0既知の問題：Klarna オンサイトメッセージングの空白ページ

ここでは、Klarnaの支払い方法に関する既知のAdobe Commerce 2.4.0の問題について説明します。この問題では、デザインテーマを指定せずにKlarnaのオンサイトメッセージを有効にすると、ストアフロントに商品ページが正しく表示されません（商品ページが空白で表示されます）。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.0
* Adobe Commerce on cloud infrastructure 2.4.0

<u>前提条件：</u> Klarna支払い方法が有効になっています。

<u>再生する手順：</u>

1. Commerce管理者で、**Stores** > **Configuration** > **Sales** > **Payment Methods** > **Klarna** > **Klarna On-Site Messaging**&#x200B;に移動します。
1. **Enable**&#x200B;を&#x200B;*Yes*&#x200B;に設定します。
1. 「**デザインテーマ**」フィールドを空白のままにします。
1. **設定を保存**&#x200B;をクリックして設定を保存します。
1. ストアフロントに移動し、任意の製品ページに移動します。

<u>期待される結果：</u>

Klarnaのオンサイトメッセージに適用されるデフォルトのデザインテーマで、ページが正常に読み込まれます。

<u>実際の結果：</u>

空白ページが表示されます。

## Solution

Klarna オンサイトメッセージを有効にする場合は、常に&#x200B;**デザインテーマ** フィールドが空白になっていないことを確認してください。
