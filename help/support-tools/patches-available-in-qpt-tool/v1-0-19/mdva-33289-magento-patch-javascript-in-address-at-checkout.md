---
title: 「MDVA-33289 パッチ：チェックアウト時のアドレスの JavaScript」
description: MDVA-33289 パッチは、支払い時に JavaScript がアドレスに表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-33289。 この問題はAdobe Commerce 2.4.3 で修正される予定だったことに注意してください。
exl-id: 247e4f05-7e89-4d37-b3d4-c2cae7595267
feature: Checkout, Marketing Tools, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# MDVA-33289 パッチ：チェックアウト時のアドレスの JavaScript

MDVA-33289 パッチは、支払い時に JavaScript がアドレスに表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.19 がインストールされている場合に使用できます。 パッチ ID は MDVA-33289。 この問題はAdobe Commerce 2.4.3 で修正される予定だったことに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** Cloud Infrastructure 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** クラウドインフラストラクチャー上のAdobe CommerceおよびオンプレミスのAdobe Commerce 2.4.0～2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Google Tag Manager （GTM）を有効にしてチェックアウトすると、JavaScript がアドレスフィールドに表示されます。

<u> 再現手順 </u>:

1. GTM を有効にします。 詳しくは、ユーザーガイドの ](https://docs.magento.com/user-guide/marketing/google-tag-manager.html)0}Google タグマネージャー } を参照してください。[
1. ストアフロントで、商品を買い物かごに追加します。
1. チェックアウトします。

<u> 実際の結果 </u>:

address セクションが更新されますが、多くの JavaScript コードテキストが含まれます。

<u> 期待される結果 </u>:

アドレスが表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
