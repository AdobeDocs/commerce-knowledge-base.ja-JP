---
title: 「MDVA-33482 パッチ：クレジット・メモの税金の計算ミス」
description: MDVA-33482 パッチは、クレジット メモで税金が誤って計算される問題を解決します。
exl-id: 80740e6f-2b6c-4770-9a1a-58ba68a1b28f
feature: Orders, Returns, Taxes
role: Admin
source-git-commit: 0ffa6d63f7046048f7e8f0e9fab1ee1869c98e93
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# MDVA-33482 パッチ：クレジット・メモの税金の計算ミス

MDVA-33482 パッチは、調整手数料または調整払い戻しが適用されていない場合にクレジット メモで税金が計算されない問題を解決します。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.15 がインストールされている場合に使用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**このパッチは、Adobe Commerce バージョン用に作成されます** Adobe Commerce on cloud infrastructure 2.4.0

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.5～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u>:

1. **税金** を設定します。
1. 任意のオンライン支払い方法を使用して、バックエンドで 2 つの製品を使用して注文を作成します（例：[!DNL PayPal Payment Pro]）。 すべての商品に税金が適用されていることを確認してください。
1. 注文の 2 つの請求書を作成します。
1. 請求書の 1 つに対してクレジット・メモを作成します。 調整手数料または調整払い戻しを適用する予定の場合、ソリューションは適用されないことに注意してください。
1. クレジット・メモ合計をチェックします。

<u> 期待される結果 </u>:

クレジット・メモには、一部請求済の税額のみが想定どおりに含まれます。

<u> 実際の結果 </u>:

税額全額がクレジット メモに表示されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
