---
title: 「MDVA-33559 パッチ：PayflowPro 支払いが拒否されましたエラー」
description: MDVA-33559 パッチは、PayPal PayflowPro の支払いが拒否される問題を解決します。
exl-id: aec57ffa-07c7-404e-985d-8ec4fdb019b1
feature: Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# MDVA-33559 パッチ：PayflowPro 支払い拒否エラー

MDVA-33559 パッチは、PayPal PayflowPro の支払いが拒否される問題を解決します。

このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.15 がインストールされている場合に使用できます。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.3.5-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.3.0～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この問題は、名前で使用されているアンパサンド記号（&amp;）と等号（=）の特殊文字に関するものです。

<u> 再現手順 </u>:

1. シンプルな製品を買い物かごに追加します。
1. チェックアウトに移動します。
1. 配送先住所を設定します。 （発送先住所の例：**名** = ** *John&#39;s* ** **姓** = ** *Apple &amp; Oranges, Inc* ** **番地** = *1234 E Nameless St* **国** = *US* **州/都道府県** = *Anystate* **** ** **** *12345* **** *1234567890*
1. 支払いを **PayPal PayflowPro** に設定し、チェックアウトを完了しようとします。

<u> 期待される結果 </u>:

トランザクションの結果、支払いが成功するか、正しいエラーメッセージが期待どおりに表示されます。

<u> 実際の結果 </u>:

トランザクションが却下され、「トランザクションが却下されました」というメールが顧客に届きます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
