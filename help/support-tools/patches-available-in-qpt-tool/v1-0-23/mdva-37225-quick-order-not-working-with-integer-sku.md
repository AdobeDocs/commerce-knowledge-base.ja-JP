---
title: 「MDVA-37225：整数 SKU でクイックオーダーが機能しない」
description: Adobe Commerceの MDVA-37225 品質パッチを適用すると、読み込まれた SKU に整数値がある場合にクイックオーダーを作成したときにページが読み込まれない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.23 がインストールされている場合に利用できます。 パッチ ID は MDVA-37225。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。
exl-id: ecd2b9d7-ca68-4372-b0c5-55e2a3301586
feature: B2B, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# MDVA-37225：整数 SKU でクイックオーダーが機能しない

Adobe Commerceの MDVA-37225 品質パッチを適用すると、読み込まれた SKU に整数値がある場合にクイックオーダーを作成したときにページが読み込まれない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.23 がインストールされている場合に使用できます。 パッチ ID は MDVA-37225。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャー 2.4.1-p1 上のAdobe Commerce用に設計されました
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.1-2.4.2-p1 とも互換性があります

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 前提条件 </u>:

B2B モジュールがインストールされたAdobe Commerce

<u> 再現手順 </u>:

1. B2B クイックオーダー機能を有効にします。
1. SKU を使用してシンプルな製品を 4 つ作成します（例：*00100*、*001E002*、*001E02C* および *7100824*）。
1. フロントエンドの ``<storefront_url>/quickorder`` ページに移動し、CSV ファイルを使用して次のサンプルコンテンツで注文を作成してみてください。

| sku | 数量 |
|---|---|
| 00100 | 1 |


<u> 期待される結果 </u>:

製品（例：SKU が *00100* の製品）が期待どおりに買い物かごに追加されます。

<u> 実際の結果 </u>:

ページは読み込まれず、商品は買い物かごに追加されません。


## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、開発者向けドキュメントの以下のリンクを使用します。

* Adobe CommerceとMagento Open Sourceオンプレミス：[Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce: [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)

## 関連資料

サポートナレッジベースの品質向上パッチツールについて詳しくは、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)

QPT ツールで使用可能なその他のパッチについて詳しくは、サポートナレッジベースの [QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
