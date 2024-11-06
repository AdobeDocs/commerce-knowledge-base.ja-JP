---
title: 「MDVA-40101：商品が注文後ミニカートのままになる PayPal Express Checkout」
description: MDVA-40101 パッチは、PayPal Express Checkout を使用して注文が成功した後、ミニカートからアイテムが削除されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/patches/overview） 1.1.4 がインストールされている場合に利用できます。 パッチ ID は MDVA-40101。 この問題はAdobe Commerce 2.4.0 で修正されました。
exl-id: d640dfcd-6fb6-4cc6-8817-3ae19aa59bed
feature: Checkout, Orders, Payments, Shopping Cart
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# MDVA-40101：商品は注文後ミニカートのままになります PayPal Express Checkout

MDVA-40101 パッチは、PayPal Express Checkout を使用して注文が成功した後、ミニカートからアイテムが削除されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/patches/overview)1.1.4 がインストールされている場合に使用できます。 パッチ ID は MDVA-40101。 この問題はAdobe Commerce 2.4.0 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.7

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.7-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

PayPal Express Checkout を使用して注文が成功した後も、商品はミニカートに残ります。

<u> 再現手順 </u>:

ブラウザーの匿名モードで PayPal Express Checkout を使用して注文します。

<u> 期待される結果 </u>:

注文が正常に完了したら、ミニカートは空にする必要があります。

<u> 実際の結果 </u>:

* 成功ページに、空のミニカートが表示されます。
* 他のすべてのページには、購入した商品を含むミニカートが表示されます。
* 買い物かごのリンクをクリックすると、空の買い物かごページにリダイレクトされる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
