---
title: '''MDVA-31399 パッチ：小計 税金）「買い物かごルールの条件」'
description: MDVA-31399 パッチは、*Subtotal （Incl. 税金）* オプションを [ 買い物かご価格ルール条件 ] （https://docs.magento.com/user-guide/v2.3/marketing/price-rules-cart-create.html#step-2-describe-the-conditions）に追加し、小計（税込）に基づいて買い物かご価格ルールを適用できなかった問題を修正しました。 （税金）番号。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.12 がインストールされている場合に利用できます。
exl-id: ea0f4060-753a-4b0d-896b-fff54ffd1a82
feature: Marketing Tools, Orders, Shopping Cart, Taxes
role: Admin
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# MDVA-31399 パッチ：小計 税金）が買い物かごルールの条件にある

MDVA-31399 パッチは *Subtotal （Incl. 税金）* オプション [ 買い物かご価格ルールの条件 ](https://docs.magento.com/user-guide/v2.3/marketing/price-rules-cart-create.html#step-2-describe-the-conditions)、小計に基づいて買い物かご価格ルールを適用できなかった問題を修正しました（税込） （税金）番号。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.12 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.2 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

小計に基づく買い物かご価格ルールを適用することはできません（税込）。 （税金）番号。

<u> 再現手順 </u>:

1. 税を含む製品価格を設定します。
1. 税務処理基準と税率を 20% に作成します。
1. **Price** = *100* （この価格は税込）の商品を作成します。
1. 小計がこれらの条件に一致する場合に$10 の固定割引を適用するには、クーポン「10off」を使用して新しい買い物かご価格ルールを作成します。

**条件**: *これらの条件がすべて TRUE の場合：*        * **小計** が 100 以上*

<u> 期待される結果 </u>:

クーポンを使用して小計カート価格ルールを作成し、税金を含む小計に割引を適用する機能があります。

<u> 実際の結果 </u>:

買い物かごルールの条件には、*小計* および *小計（除）の 2 つのオプションがあります。 （税金）* 選択した場合は、税金を除く小計にのみルールが適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
