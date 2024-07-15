---
title: 「Adobe Commerce 2.3.7-p1 の既知の問題：PayPal の古い注文合計」
description: 「この記事では、Adobe Commerce 2.3.7-p1 の既知の問題に対するパッチを提供します。PayPal チェックアウトを複数回使用する場合、お客様は、新しい商品を注文するのではなく、以前に注文した商品を買い物かごに入れます。」
exl-id: ceb8f7ad-0cf7-4d42-aded-25d1dd947f5b
feature: Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Adobe Commerce 2.3.7-p1 の既知の問題：PayPal の注文合計が古い

この記事では、Adobe Commerce 2.3.7-p1 の既知の問題に対するパッチを提供します。PayPal チェックアウトを複数回使用する場合、お客様は、新しい商品を注文するのではなく、以前に注文した商品を買い物かごに入れます。
この記事からパッチをダウンロードできます。また、Quality Patches Tool （QPT）からも入手できます。

## 影響を受けるバージョン

* Adobe Commerce（すべてのデプロイメントオプション） 2.3.7-p1
* Magento Open Source 2.3.7-p1

## 問題

PayPal Express のチェックアウト支払い方法を使用して注文を行う場合、実際の製品ではなく、以前に注文した購入製品が注文に追加されます。

<u> 再現手順：</u>

1. ストアフロントで、商品を買い物かごに追加します（製品 A、価格$50）。
1. 買い物かごリンクをクリックして、買い物かごを開きます。
1. 「**PayPal チェックアウト**」ボタンをクリックします。
1. PayPal の認証情報を使用して PayPal にログインし、支払いを送信します。
1. 店舗側での注文の配置を完了します。
1. カタログに戻り、別の製品（製品 B、価格$100）を買い物かごに追加します。
1. 買い物かごリンクをクリックして、買い物かごを開きます。
1. 「**PayPal チェックアウト**」ボタンをクリックします。

<u> 実際の結果：</u>

カートの製品価格は 100 ドルではなく 50 ドルです。<br/>
店舗側では、注文に製品 B ではなく製品 A が含まれます。

<u> 期待される結果：</u>

製品 B が注文に追加されます。

## 解決策

この記事で提供されているパッチを適用します。

## パッチ

次のリンクを使用して、パッチを含んだ.zip ファイルをダウンロードします：[MC42674-composer.patch.zip](assets/MC42674-composer.patch.zip)。

### 互換性のあるAdobe Commerce バージョン

* Adobe Commerce（すべてのデプロイメントオプション） 2.3.7-p1

## パッチの適用方法

1. ダウンロードした.zip ファイルを解凍します。
1. 詳しくは、[Adobe提供のコンポーザーパッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。
