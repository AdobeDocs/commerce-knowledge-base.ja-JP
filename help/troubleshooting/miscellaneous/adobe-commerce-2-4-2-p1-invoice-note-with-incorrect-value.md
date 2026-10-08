---
title: Adobe Commerce 2.4.2-p1：誤った値の請求書メモ
description: この記事では、注文の作成中にカスタマーグループが変更されたときに、誤った値の請求書メモが生成される既知のAdobe Commerce 2.4.2-p1の問題について説明します。 この問題は、バージョン 2.4.3で修正されています。
exl-id: bde90251-625f-4c9d-8e5a-9a2019656125
feature: Customer Service, Invoices
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%
---
# Adobe Commerce 2.4.2-p1：誤った値の請求書メモ

この記事では、注文の作成中にカスタマーグループが変更されたときに、誤った値の請求書メモが生成される既知のAdobe Commerce 2.4.2-p1の問題について説明します。 この問題は、バージョン 2.4.3で修正されています。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.2-p1
* Adobe Commerce on cloud infrastructure 2.4.2-p1

## イシュー

注文の作成時に顧客グループが変更されると、誤った請求書メモが付いた請求書が生成されます。

<u>複製する手順</u>:

1. **テスト顧客アカウント**&#x200B;を作成し、**小売顧客グループ**&#x200B;に追加します。
1. テスト顧客の&#x200B;**新規注文**&#x200B;を作成し、**製品**&#x200B;および&#x200B;**住所**&#x200B;を追加します。
1. **配送方法**&#x200B;を選択します。
1. **Account Information** セクションで、Customer Groupを&#x200B;**Government**&#x200B;から&#x200B;**Retailer**&#x200B;に変更します。
1. 「**注文を配置**」をクリックします。
1. 「**請求書**」 > 「**請求書を送信**」をクリックします。

<u>期待される結果</u>:

以下のメモは、この注文の&#x200B;**メモ** セクションの「Vertex Invoice sent successfully.」に表示されます。 金額：$0.00&quot;

<u>実際の結果</u>:

次のメモは、この注文&#x200B;**の「** メモ」セクションに表示されます。「Vertex Invoice sent successfully. 金額：3.23 ドル。」

## Solution

この問題は、バージョン 2.4.3で修正されています。
