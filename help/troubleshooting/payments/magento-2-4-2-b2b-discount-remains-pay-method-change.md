---
title: Adobe Commerce 2.4.2 B2B：割引は引き続き支払い方法の変更
description: この記事では、チェックアウト時に支払い方法が変更された後も支払い方法と関連付けられた割引が持続する、既知のAdobe Commerce 2.4.2 B2Bの問題について説明します。 現在利用できる解決策はありません。
exl-id: cd863852-403b-404f-8717-c78c238f5f33
feature: B2B, Orders, Payments, Personalization
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Adobe Commerce 2.4.2 B2B：割引は引き続き支払い方法の変更

この記事では、チェックアウト時に支払い方法が変更された後も支払い方法と関連付けられた割引が持続する、既知のAdobe Commerce 2.4.2 B2Bの問題について説明します。 現在利用できる解決策はありません。

## 影響を受ける製品とバージョン

* Adobe Commerce 2.4.2
* Adobe Commerce on cloud infrastructure 2.4.2
* Adobe Commerce 1.3.1向けB2B


## イシュー

<u>複製する手順</u> :

1. 支払い方法に関連付けられたカート **価格ルール**&#x200B;を作成します（例：Paypal ユーザーは20%の割引を受けます）。
1. 発注書（PO）を作成し、支払い方法として「Paypal」を選択します。 割引が適用されます。
1. POが承認されました。
1. 支払いページに移動して注文を完了します。
1. 別の決済方法を選択してください。

<u>実際の結果</u> :

支払い方法の割引は、注文合計に引き続き適用されます。  エラーメッセージは表示されません。ストア所有者は、注文履歴を確認することで、この問題が発生したことを確認できます。

<u>期待される結果</u> 予想通り、:The支払い方法の割引が注文合計から削除されます。

## Solution

現在利用できる解決策はありません。
