---
title: 広告ブロッカーが有効な場合にチェックアウトページが読み込まれない
description: この記事では、uBlock またはその他の広告ブロッカーによってチェックアウトページが読み込まれなかった場合に発生する、Adobe Commerce on cloud infrastructure 2.2.2 の既知の問題に対するパッチを提供します。
exl-id: fe718f21-df23-4ab1-a6b0-03bad4d7095d
feature: Checkout, Orders
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 広告ブロッカーが有効な場合にチェックアウトページが読み込まれない

この記事では、uBlock またはその他の広告ブロッカーによってチェックアウトページが読み込まれなかった場合に発生する、Adobe Commerce on cloud infrastructure 2.2.2 の既知の問題に対するパッチを提供します。

## 問題

ストアでGoogle Analyticsが有効になっている場合、uBlock またはその他の広告ブロッカーがインストールされているお客様がチェックアウトに進むと、 `trackingCode.js` ファイルの読み込みがブロックされ、RequireJS が JS 実行フローを中断する。 これにより、チェックアウトページの読み込みに関して問題が発生します。

<u>再現手順</u> :

前提条件：ブラウザーに広告ブロッカーをインストールしてアクティブにする必要があります。

1. Commerce Admin で、Google Analytics機能を有効にして設定します。
1. ストアフロントで製品ページを開きます。
1. 商品を買い物かごに追加します。
1. 「」をクリックします **チェックアウトに移動** リンク。

<u>期待される結果</u>：チェックアウトページが読み込まれ、顧客がチェックアウトを完了できます。

<u>実際の結果</u>：チェックアウトページが読み込まれず、読み込みスピナーが消えない。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-9353\_EE\_2.2.2\_v1.composer.patch のダウンロード](assets/MDVA-9353_EE_2.2.2_v1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー 2.2.2 上のAdobe Commerce

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerce（2.1.0 から 2.1.14）
* クラウドインフラストラクチャー上のAdobe Commerce（2.2.0 から 2.2.1 および 2.2.3 から 2.2.5 へ）
* Adobe Commerceオンプレミス（2.1.0 から 2.1.14 まで）
* Adobe Commerce オンプレミスを 2.2.0 から 2.2.5 に

## パッチの適用方法

手順については、を参照してください [Adobeが提供する composer パッチの適用方法](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) サポートナレッジベースで。

## 役に立つリンク

* [GitHub で取り上げた問題](https://github.com/magento/magento2/pull/13061)

## 添付ファイル
