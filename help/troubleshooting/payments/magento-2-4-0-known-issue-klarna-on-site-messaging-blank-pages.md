---
title: Adobe Commerce 2.4.0既知の問題：Klarna オンサイトメッセージングの空白ページ
description: ここでは、Klarnaの支払い方法に関する既知のAdobe Commerce 2.4.0の問題について説明します。この問題では、デザインテーマを指定せずにKlarnaのオンサイトメッセージを有効にすると、ストアフロントに商品ページが正しく表示されません（商品ページが空白で表示されます）。
exl-id: f0f9edfc-eaad-4947-9200-41e217bfbe84
feature: Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
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
