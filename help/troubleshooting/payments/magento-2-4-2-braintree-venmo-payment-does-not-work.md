---
title: 「Adobe Commerce 2.4.2:BraintreeVenmo の支払いが機能しない」
description: この記事では、チェックアウト時にBraintree Venmo を使用しても注文が生成されない、Adobe Commerce 2.4.2 の既知の問題について説明します。 現在、利用可能な解決策はありません。
exl-id: 1832ab64-5024-444b-915e-473b34979a6e
feature: Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Adobe Commerce 2.4.2:BraintreeVenmo の支払いが機能しない

この記事では、チェックアウト時にBraintree Venmo を使用しても注文が生成されない、Adobe Commerce 2.4.2 の既知の問題について説明します。 現在、利用可能な解決策はありません。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

## 問題

<u> 事前条件 </u> :

Braintree設定で Venmo 支払いを有効にします。

<u> 再現手順 </u> :

1. ストアフロントで、任意の項目を買い物かごに追加します。
1. **チェックアウト** に進みます。
1. 適切な発送方法を選択します。
1. 支払方法として **Venmo** を選択します。
1. **Venmo で支払う** をクリックします。
1. **注文する** をクリックします。

<u> 実際の結果 </u>:

ユーザーが Venmo アプリからストアにリダイレクトされて戻った後も、注文がAdobe Commerce コードで作成されず、エラーメッセージは表示されません。 注文はBraintreeで作成されます。

<u> 期待される結果 </u>:

注文は、お客様が Venmo アプリからストアにリダイレクトされ直した後にAdobe Commerceで作成され、期待どおりにBraintreeで作成されます。

## 解決策

現在、利用可能な解決策はありません。
