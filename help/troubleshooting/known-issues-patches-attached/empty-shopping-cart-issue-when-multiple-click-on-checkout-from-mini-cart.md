---
title: ミニ買い物かごからチェックアウトを複数クリックした際の空の買い物かご問題
description: この記事では、ミニ買い物かごで顧客が**チェックアウトに移動**を複数回クリックした後に買い物かごが空になるという、Adobe Commerce 2.2.3 の既知の問題に対するパッチを提供します。
exl-id: 06b82c91-8998-4e7b-9fc0-671c9b2a2d3f
feature: Checkout, Orders, Shopping Cart
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# ミニ買い物かごからチェックアウトを複数クリックした際の空の買い物かご問題

この記事では、ミニ買い物かごで顧客が **チェックアウトに移動** を複数回クリックした後に買い物かごが空になるという、Adobe Commerce 2.2.3 の既知の問題に対するパッチを提供します。

## 問題

顧客は商品を買い物かごに追加し、「**チェックアウトに移動**」ボタンを数回クリックしてチェックアウトしようとしますが、買い物かごに移動すると、買い物かごは空になります。 ミニカートに商品が表示される場合があります。

<u> 再現手順 </u> :

1. 店頭で商品ページを開きます。
1. 商品を買い物かごに追加します。
1. ミニ買い物かごで、「チェックアウトに移動 **を数回クリックし** す。

<u> 期待される結果 </u> :

カートには、追加したすべての製品が含まれています。

<u> 実際の結果 </u> :

買い物かごにアイテムがありません。

## パッチ

パッチはこの記事に添付されています。 パッチをダウンロードするには、記事の最後までスクロールして必要なファイル名をクリックするか、次のいずれかのリンクをクリックします。

[MDVA-10441\_EE\_2.2.3\_v3.composer.patch のダウンロード](assets/MDVA-10441_EE_2.2.3_v3.composer.patch.zip)

[MDVA-17078\_EE\_2.2.5\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-17078_EE_2.2.5_COMPOSER_v1.patch.zip)

### 互換性のあるAdobe Commerce バージョン

パッチは次の場合に作成されました。

* Adobe Commerce オンプレミス 2.2.3 （`MDVA-10441_EE_2.2.3_v3.composer.patch` ファイル）
* クラウドインフラストラクチャー 2.2.5 上のAdobe Commerce（`MDVA-17078_EE_2.2.5_COMPOSER_v1.patch` ファイル）

`MDVA-10441_EE_2.2.3_v3.composer.patch` のパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決する可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerceのバージョン 2.2.1 から 2.2.5 まで
* Adobe Commerce オンプレミスのバージョン（2.2.1 から 2.2.5 まで）

`MDVA-17078_EE_2.2.5_COMPOSER_v1.patch` のパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決する可能性があります）。

* Adobe Commerce 2.2.5

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
