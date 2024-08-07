---
title: 「MDVA-37779:GraphQL経由で設定可能な商品を買い物かごに追加できない」
description: MDVA-37779 Adobe Commerce パッチでは、Web サイト ID がストア ID と異なる場合に、設定可能な商品を買い物かごに追加できないという問題を解決しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.24 がインストールされている場合に利用できます。 パッチ ID は MDVA-37779。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。 
exl-id: 5f344896-39c3-4e17-89b8-1b987bae2968
feature: GraphQL, Configuration, Orders, Products, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# MDVA-37779:GraphQL経由で設定可能な商品を買い物かごに追加できない

MDVA-37779 Adobe Commerce パッチでは、Web サイト ID がストア ID と異なる場合に、設定可能な商品を買い物かごに追加できないという問題を解決しました。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.24 がインストールされている場合に使用できます。 パッチ ID は MDVA-37779。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.2 - 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

web サイト ID がストア ID と異なる場合、設定可能な製品を買い物かごに追加することはできません。

<u> 前提条件 </u>:

2 つ目の web サイト、ストア、ストアを表示します。web サイトの ID がストア ID と異なります。

<u> 再現手順 </u>:

1. GraphQl mutation `createEmptyCart` を使用して、空の買い物かごを作成します。
1. `addConfigurableProductsToCart` ミューテーションを使用して、設定可能な製品を買い物かごに追加してみてください。

<u> 期待される結果 </u>:

商品が買い物かごに追加されました。

<u> 実際の結果 </u>:

エラーが表示されます：*SKU xxxx の製品を買い物かごに追加できませんでした：リクエストされた ID 3 の web サイトが見つかりませんでした。 Web サイトを確認して、もう一度試してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。


## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
