---
title: 同名の製品の CSV 製品情報の読み込みに失敗します
description: ここでは、同じ名前の商品が存在する場合に、商品情報を含んだ「.csv」ファイルを読み込もうとするとエラーが発生する、Adobe Commerce 2.2.3 の既知の問題に対するパッチを提供します。
exl-id: 420b0283-455a-4bd5-ba51-18f341ddacd5
feature: Data Import/Export, Products
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 同名の製品の CSV 製品情報の読み込みに失敗します

ここでは、同じ名前の商品が存在する場合に、商品情報を含む `.csv` ファイルを読み込もうとするとエラーが発生する、Adobe Commerce 2.2.3 の既知の問題に対するパッチを提供します。

## 問題

商品情報を含む `.csv` ファイルが読み込まれたとき、同じ名前の商品がある場合、データを確認手順で「*」`URL Key XYZ was already generated for an item with the SKU %sku%"`* というエラーが発生します。 この問題は、読み込んだ `.csv` ファイルに製品の URL の列がない場合でも、読み込み中に製品の URL を書き換えることで発生します。

<u> 再現手順 </u>:

1. Commerce Admin で、同じ名前の 2 つの設定可能な商品を作成します。
1. `.csv` ファイルを作成して、これらの製品のデータを読み込みます。例えば、次の列があります。`sku` | `product_type` | `name` | `product_websites` | `store_view_code`
1. **システム**/**データ転送**/**インポート** に移動し、`.csv` ファイルを選択します。
1. **データを確認** をクリックします。

<u> 期待される結果 </u>:

問題は見つかりませんでした。`.csv` ファイルを正常にインポートできます。

<u> 実際の結果 </u>:

次のエラーメッセージが表示されます。*「URL キー XYZ は、SKU が %sku% の項目に対して既に生成されました」* ファイルを読み込めません。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-12899\_EE\_2.2.3\_COMPOSER\_v2.patch のダウンロード](assets/MDVA-12899_EE_2.2.3_COMPOSER_v2.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* Adobe Commerce オンプレミス 2.2.3

このパッチは、次のAdobe Commerceのエディションとバージョンとも互換性があります（ただし、問題が解決する可能性はありません）。

* クラウドインフラストラクチャー上のAdobe Commerce（2.2.0 から 2.2.7 および 2.3.0）
* Adobe Commerce オンプレミス（2.2.0 から 2.2.2、2.2.4 から 2.2.7、および 2.3.0）

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 役に立つリンク

[ クラウドインフラストラクチャー上のAdobe Commerceにカスタムパッチを適用 ](https://devdocs.magento.com/guides/v2.3/cloud/project/project-patch.html)

## 添付ファイル
