---
title: 「MDVA-40101：商品が注文後ミニカートのままになる PayPal Express Checkout」
description: MDVA-40101 パッチは、PayPal Express Checkout を使用して注文が成功した後、ミニカートからアイテムが削除されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.4 がインストールされている場合に利用できます。 パッチ ID は MDVA-40101。 この問題はAdobe Commerce 2.4.0 で修正されました。
exl-id: d640dfcd-6fb6-4cc6-8817-3ae19aa59bed
feature: Checkout, Orders, Payments, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# MDVA-40101：商品は注文後ミニカートのままになります PayPal Express Checkout

MDVA-40101 パッチは、PayPal Express Checkout を使用して注文が成功した後、ミニカートからアイテムが削除されない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.4 がインストールされています。 パッチ ID は MDVA-40101。 この問題はAdobe Commerce 2.4.0 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.7

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.7-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

PayPal Express Checkout を使用して注文が成功した後も、商品はミニカートに残ります。

<u>再現手順</u>:

ブラウザーの匿名モードで PayPal Express Checkout を使用して注文します。

<u>期待される結果</u>:

注文が正常に完了したら、ミニカートは空にする必要があります。

<u>実際の結果</u>:

* 成功ページに、空のミニカートが表示されます。
* 他のすべてのページには、購入した商品を含むミニカートが表示されます。
* 買い物かごのリンクをクリックすると、空の買い物かごページにリダイレクトされる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
