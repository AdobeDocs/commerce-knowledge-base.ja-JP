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

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.15 がインストールされています。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.5 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 設定 **税金**.
1. 任意のオンライン支払い方法を使用して、バックエンドで 2 つの製品を使用して注文を作成します（例： [!DNL PayPal Payment Pro]）に設定します。 すべての商品に税金が適用されていることを確認してください。
1. 注文の 2 つの請求書を作成します。
1. 請求書の 1 つに対してクレジット・メモを作成します。 調整手数料または調整払い戻しを適用する予定の場合、ソリューションは適用されないことに注意してください。
1. クレジット・メモ合計をチェックします。

<u>期待される結果</u>:

クレジット・メモには、一部請求済の税額のみが想定どおりに含まれます。

<u>実際の結果</u>:

税額全額がクレジット メモに表示されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
