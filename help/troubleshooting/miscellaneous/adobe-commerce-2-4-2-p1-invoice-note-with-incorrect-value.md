---
title: 「Adobe Commerce 2.4.2-p1：間違った値の請求書メモ」
description: ここでは、Adobe Commerce 2.4.2-p1 の既知の問題について説明します。この問題では、注文の作成中にお客様のグループが変更されると、値が正しくない請求書が生成されます。 この問題は、バージョン 2.4.3 で修正されました。
exl-id: bde90251-625f-4c9d-8e5a-9a2019656125
feature: Customer Service, Invoices
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Adobe Commerce 2.4.2-p1：誤った値を含む請求書メモ

ここでは、Adobe Commerce 2.4.2-p1 の既知の問題について説明します。この問題では、注文の作成中にお客様のグループが変更されると、値が正しくない請求書が生成されます。 この問題は、バージョン 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.2-p1
* クラウドインフラストラクチャー上のAdobe Commerce 2.4.2-p1

## 問題

注文の作成時に顧客グループが変更されると、請求書は誤った請求書メモで生成されます。

<u>再現手順</u>:

1. を作成 **顧客アカウントのテスト** を作成して、に追加します **小売顧客グループ**.
1. を作成 **新しい注文** テスト顧客として、次を追加します **製品** および **住所**.
1. を選択 **発送方法**.
1. が含まれる **アカウント情報** セクション、顧客グループを変更 **小売業者** 対象： **政府**.
1. クリック **注文する**.
1. クリック **請求書** > **請求書の送信**.

<u>期待される結果</u>:

の下に次のメモが表示されます。 **この注文のメモ**  セクション：「頂点請求書が正常に送信されました。 金額：0.00 ドル。」

<u>実際の結果</u>:

次のメモがの下に表示されます **この注文のメモ** セクション：「頂点請求書が正常に送信されました。 金額：3.23 ドル。」

## 解決策

この問題は、バージョン 2.4.3 で修正されました。
