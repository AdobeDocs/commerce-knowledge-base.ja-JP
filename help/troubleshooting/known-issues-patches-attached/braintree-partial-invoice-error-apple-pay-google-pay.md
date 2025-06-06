---
title: 「Adobe Commerce 2.4.4：部分請求書を作成できない」
description: この記事では、お支払い方法としてApple Pay またはGoogle Pay through Braintreeを使用すると、請求書の一部を作成できない問題のホットフィックスを提供します。
exl-id: bf78cc07-9dc7-4eb8-bfdf-57ea5131effb
feature: Invoices, Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Adobe Commerce 2.4.4：部分請求書を作成できない

この記事では、お支払い方法としてApple Pay またはGoogle Pay through Braintreeを使用すると、請求書の一部を作成できない問題のホットフィックスを提供します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.4

## 問題

支払い方法としてApple Pay またはGoogle Pay を使用すると、「*「vault_capture」コマンドが存在しません。 コマンドを確認し、もう一度試してください。部分請求書の作成中に*」が表示されます。

<u> 再現手順 </u>:

1. Adobe Commerce web サイトを開きます。
1. シンプルな商品を買い物かごに追加します（数量 2）。
1. 買い物かごからの支払い方法として **0&rbrace;Apple Pay** または **Google Pay&rbrace; を選択します。**
1. 注文します。
1. バックエンドから注文の詳細を開きます。
1. 部分請求書を作成します。
1. 残額に対して別の請求書を作成します。

<u> 期待される結果 </u>:

部分請求書が作成されます。

<u> 実際の結果 </u>:

最初の部分請求書が作成されます。 2 通目の部分請求書を作成すると、次のエラーが表示されます。*「vault_capture」コマンドが存在しません。 コマンドを確認して、もう一度試してください*。

## 原因：

Adobe Commerceでは、クレジットカードの詳細が Vault に保存され、部分請求書が作成されます。 現在、Apple Pay とGoogle Pay をヴォールティングする機能はありません。

## 解決策

この問題を解決するには、次のパッチを適用します。

[Braintree_disabled_partial_capture_for_applepay_googlepay.zip](assets/braintree-disabled-partial-capture-for-applepay-googlepay.zip)

## パッチの適用方法

手順については、[Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。
