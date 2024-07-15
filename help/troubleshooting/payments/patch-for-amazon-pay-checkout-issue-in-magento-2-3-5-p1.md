---
title: Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ
description: このパッチにより、Adobe CommerceでAmazon Pay にチェックアウトしている際に、支払いウィジェットから「確認と支払い」ステップで支払い方法を変更できないという問題が解決されます。
exl-id: a241f67f-019c-4ff2-a5ad-e7dc71639768
feature: Checkout, Orders, Payments
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Adobe Commerce 2.3.5-p1 でのAmazon Pay チェックアウトの問題に対するパッチ

このパッチにより、Adobe CommerceでAmazon Pay にチェックアウトしている際に、支払いウィジェットから「確認と支払い」ステップで支払い方法を変更できないという問題が解決されます。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャバージョン 2.3.5-p1 上のAdobe Commerce
* Adobe Commerce オンプレミス バージョン 2.3.5-p1

## 問題

買い物客がAmazon Pay でチェックアウトし、ログインして支払い手順に進み、支払いウィジェットから支払いクレジットカードを変更しようとすると、エラーメッセージが表示されます。 買い物客がエラーを無視してチェックアウトに進む場合、チェックアウトは完了できません。

この問題を解決し、エラーを削除するために、[patch](assets/BUNDLE-2554_EE_2.3.5-p1.composer.patch.zip) を作成しました。

<u> 再現手順 </u>:

1. Amazon Pay でチェックアウトを開始します。
1. Amazon Pay のお客様としてログインします。
1. 配送方法を選択し、支払い手順に進みます。
1. クレジットカードを別のカードに変更してみてください。

<u> 期待される結果 </u>：エラーのない支払い方法として、別のクレジットカードが選択されています。

<u> 実際の結果 </u>：次のエラーメッセージが表示されます。*「注文を完了するには、このマーチャントにお問い合わせください」*

## 解決策

以下で [ パッチを適用 ](assets/BUNDLE-2554_EE_2.3.5-p1.composer.patch.zip) します。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[BUNDLE-2554\_EE\_2.3.5-p1.composer.patch をダウンロード](assets/BUNDLE-2554_EE_2.3.5-p1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャバージョン 2.3.5-p1 上のAdobe Commerce
* Adobe Commerce オンプレミス バージョン 2.3.5-p1

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* Adobe Commerce on cloud infrastructure バージョン 2.3.5
* Adobe Commerce オンプレミス バージョン 2.3.5

## パッチの適用方法

手順については、サポートナレッジベースの [Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
