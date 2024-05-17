---
title: 「MDVA-33992：卸売業者の B2B カスタム価格が買い物かごに表示されない」
description: MDVA-33992 パッチは、B2B 顧客のカスタム価格が商品が買い物かごに追加された際に反映されない問題を修正します。 このパッチは、Quality Patches Tool （QPT） 1.0.15 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: 6018fae6-762c-46c6-9497-ecf090115b7f
feature: B2B, Catalog Management, Orders, Shopping Cart
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# MDVA-33992：卸売業者が買い物かごに表示されない B2B カスタム価格

MDVA-33992 パッチは、B2B 顧客のカスタム価格が商品が買い物かごに追加された際に反映されない問題を修正します。 このパッチは、Quality Patches Tool （QPT） 1.0.15 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** B2B を使用したクラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0-2.4.1-p1 （B2B 搭載）

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

B2B 顧客のカスタム価格は、製品が買い物かごに追加された際に反映されません。

<u>再現手順</u>:

この問題は、共有カタログが有効になっている B2B バージョンでも再現できます。

1. カスタムの共有カタログが割り当てられた B2B 会社を作成します。
1. 会社のカスタムカタログに、カスタム価格（階層価格）で製品を作成します。
1. B2B のお客様は、カスタム製品価格がカタログに表示されていることを確認します。
1. B2B のお客様は、商品を買い物かごに追加します。

<u>期待される結果</u>:

正しい価格が買い物かごに表示され、カタログの価格と一致します。

<u>実際の結果</u>:

カスタム価格が消え、デフォルトカタログの通常の価格が表示されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
