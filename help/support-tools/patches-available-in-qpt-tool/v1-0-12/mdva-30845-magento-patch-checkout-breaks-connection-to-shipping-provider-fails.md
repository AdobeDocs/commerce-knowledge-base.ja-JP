---
title: 「MDVA-30845：チェックアウトで配送業者への接続が失敗する」
description: MDVA-30845 パッチでは、チェックアウト時に UPS XML/USPS/DHL に接続できない場合に「Sorry, no quote are available for this order at this time*」というエラーが表示され、他の配送方法がない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.12 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正される予定であることに注意してください。
exl-id: 7be54213-1762-431b-bd3b-080c3d45f492
feature: Checkout, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# MDVA-30845：チェックアウトが原因で配送業者への接続に失敗する

MDVA-30845 パッチにより、 *申し訳ありませんが、現在この注文で利用できる見積もりはありません* チェックアウト時に UPS XML/USPS/DHL への接続に失敗するとエラーが表示され、他の配送方法はありません。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.12 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.3.5-p2 上のAdobe Commerce。

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.5-2.3.6.

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

チェックアウト中、 *申し訳ありませんが、現在この注文で利用できる見積もりはありません* ups XML/USPS/DHL への接続に失敗するとエラーが表示され、他の配送方法は利用できません。

<u>再現手順：</u>

1. 商品を作成します。
1. UPS XML 出荷方法を有効にして構成します。
1. 商品を店頭で買い物かごに追加します。
1. UPS の配送方法と定額配送が利用できることを確認します。
1. USP がゲートウェイに接続できないように、hosts ファイルを編集します。
1. 店舗正面で、料金を取得し、もう一度チェックアウトに進みます。

<u>実際の結果：</u>

*申し訳ありませんが、現在この注文で利用できる見積もりはありません* エラーが表示され、定額配送は利用できません。

<u>期待される結果：</u>

エラーメッセージは表示されず、定額配送を利用できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。


## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
