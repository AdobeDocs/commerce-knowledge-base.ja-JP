---
title: Adobe Commerce 2.4.2:Braintree Venmoの支払いが機能しない
description: この記事では、チェックアウト時にBraintree Venmoを使用する際に注文が生成されない、既知のAdobe Commerce 2.4.2の問題について説明します。 現在利用できる解決策はありません。
exl-id: 1832ab64-5024-444b-915e-473b34979a6e
feature: Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Adobe Commerce 2.4.2:Braintree Venmoの支払いが機能しない

この記事では、チェックアウト時にBraintree Venmoを使用する際に注文が生成されない、既知のAdobe Commerce 2.4.2の問題について説明します。 現在利用できる解決策はありません。

## 影響を受ける製品とバージョン

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

## イシュー

<u>前提条件</u> :

Braintree設定でVenmo支払いを有効にします。

<u>複製する手順</u> :

1. ストアフロントでショッピングカートに商品を追加します。
1. **チェックアウト**&#x200B;に進みます。
1. 適切な配送方法を選択してください。
1. 支払い方法として&#x200B;**Venmo**&#x200B;を選択します。
1. 「**Venmoでのお支払い**」をクリックします。
1. 「**注文を配置**」をクリックします。

<u>実際の結果</u>:

お客様がVenmo アプリからストアにリダイレクトされた後、注文はAdobe Commerce コードで作成されず、エラーメッセージは表示されません。 注文はBraintreeで作成されます。

<u>期待される結果</u>:

注文は、お客様がVenmo アプリから店舗にリダイレクトされた後、Adobe Commerceで作成され、注文はBraintreeで作成されます（想定どおり）。

## Solution

現在利用できる解決策はありません。
