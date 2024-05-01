---
title: 「MDVA-34943：クイックオーダーで 2 つ以上の製品を買い物かごに追加できない」
description: MDVA-34943 パッチを使用すると、クイックオーダーで買い物かごに 2 つ以上の商品を追加できない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.17 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。
exl-id: fcff6a78-fe00-4352-b0bc-149bd411d999
feature: Orders, Products, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# MDVA-34943: クイックオーダーで 2 つ以上の製品を買い物かごに追加できない

MDVA-34943 パッチを使用すると、クイックオーダーで買い物かごに 2 つ以上の商品を追加できない問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.17 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.4.0-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーが 2 つ以上の製品をクイックオーダーで買い物かごに追加できません。

<u>前提条件</u>:

シンプルな商品のAdobe Commerce。

<u>再現手順</u>:

1. に移動 **クイック注文** （ログインしていない間）ストアフロントで。
1. 有効な SKU を入力し、オートコンプリートフィールドに表示される製品をクリックして設定します **数量** = *1*.
1. 同じ有効な SKU を入力し、最初の文字の大文字と小文字を変更（大文字から小文字への変更、または小文字から大文字への変更）して、オートコンプリートフィールドに表示される製品をクリックして設定します **数量** = *1*.
1. を入力 `random_sting_value` （用） **SKU**、およびを設定 **数量** = *1*.
1. を設定 **SKU** = *123123123*、およびを設定 **数量** = *1*.
1. に最初に追加したエントリ以外はすべて削除します **クイック注文** ページ。
1. で最初の SKU （上記の手順 2 と同様）を入力します。 **複数の SKU を入力** フィールドをクリックし、 **リストに追加**.
1. これにより、最初の SKU の数量が 2、の行になります `random_sting_value`.
1. さらにテストするには、ページを更新します。
1. その結果、期待どおりにクイックオーダーの SKU がなくなります。
1. を入力 `random_sting_value2` を、に追加します。 **複数の SKU を入力** フィールドをクリックし、 **リストに追加**.
1. その結果、およびの前の 2 つの有効な SKU が得られます。 `random_sting_value2`.

<u>期待される結果</u>:

2 つ以上の製品を、期待どおりに買い物かごに追加できます。

<u>実際の結果</u>:

に移動した場合 **カート** ページに最初に追加された製品は通常どおり表示されますが、2 番目の製品とそれに続く製品が買い物かごに追加されると、「*1 製品には注意が必要です*「」エラーメッセージが表示されます。 2 番目の製品または追加の製品が **注意が必要な製品** の節 **カート** ページ。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
