---
title: '''MDVA-31399 パッチ：小計 税金）「買い物かごルールの条件」'
description: MDVA-31399 パッチは、*Subtotal （Incl. 税金）* オプションを [ 買い物かご価格ルール条件 ] （https://docs.magento.com/user-guide/v2.3/marketing/price-rules-cart-create.html#step-2-describe-the-conditions）に追加し、小計（税込）に基づいて買い物かご価格ルールを適用できなかった問題を修正しました。 （税金）番号。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.12 がインストールされている場合に利用できます。
exl-id: ea0f4060-753a-4b0d-896b-fff54ffd1a82
feature: Marketing Tools, Orders, Shopping Cart, Taxes
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# MDVA-31399 パッチ：小計 税金）が買い物かごルールの条件にある

MDVA-31399 パッチは、 *小計 税）* 対するオプション [買い物かご価格ルールの条件](https://docs.magento.com/user-guide/v2.3/marketing/price-rules-cart-create.html#step-2-describe-the-conditions)、小計に基づいて買い物かごの価格ルールを適用できなかった問題を修正しました（ （税金）番号。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.12 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.2 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

小計に基づく買い物かご価格ルールを適用することはできません（税込）。 （税金）番号。

<u>再現手順</u>:

1. 税を含む製品価格を設定します。
1. 税務処理基準と税率を 20% に作成します。
1. を使用した製品の作成 **価格** = *100* （税込み）
1. 小計がこれらの条件に一致する場合に$10 の固定割引を適用するには、クーポン「10off」を使用して新しい買い物かご価格ルールを作成します。

**条件**: *これらの条件がすべて TRUE の場合：*        * **小計** 100 以上*

<u>期待される結果</u>:

クーポンを使用して小計カート価格ルールを作成し、税金を含む小計に割引を適用する機能があります。

<u>実際の結果</u>:

買い物かごルールの条件には、次の 2 つのオプションがあります。 *小計* および *小計 税）*&#x200B;いずれを選択しても、ルールは税を除く小計にのみ適用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
