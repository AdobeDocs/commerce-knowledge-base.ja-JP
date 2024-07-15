---
title: 「MDVA-37068：仮想製品のチェックアウトで表示される税金が正しくない」
description: MDVA-37068 パッチは、チェックアウトページに仮想製品の誤った税率が表示される場合の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.26 がインストールされている場合に利用できます。 パッチ ID は MDVA-37068。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: ef75b41e-e79d-4947-8b74-87966642f808
feature: Cache, Checkout, Orders, Products, Taxes
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# MDVA-37068：仮想製品のチェックアウト時に表示される税金が正しくない

MDVA-37068 パッチは、チェックアウトページに仮想製品の誤った税率が表示される場合の問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.26 がインストールされている場合に使用できます。 パッチ ID は MDVA-37068。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce（すべてのデプロイメント方法） 2.3.1-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

買い物かごに仮想商品のみが含まれている場合、チェックアウトページに誤った税率が表示される。

<u> 前提条件 </u>:

1. 2 つの異なる国に対して 2 つの税率と税務処理基準（10% と 1% など）を個別に作成します。
1. 仮想製品を作成します。
1. 再インデックスとキャッシュのクリーンアップを実行します。

<u> 再現手順 </u>:

1. 顧客を作成します。
1. 別の請求先住所と配送先住所を追加します。
1. 仮想商品を買い物かごに追加します。
1. 「買い物かごおよびチェックアウト」ページを確認します。

<u> 期待される結果 </u>:

カートとチェックアウトページに表示される税金は同じです。

<u> 実際の結果 </u>:

買い物かごとチェックアウトページに表示される税金が異なる。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
