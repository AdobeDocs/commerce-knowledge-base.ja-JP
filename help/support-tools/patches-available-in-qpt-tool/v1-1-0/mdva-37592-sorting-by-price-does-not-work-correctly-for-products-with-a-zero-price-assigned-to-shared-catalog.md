---
title: 「MDVA-37592：価格が 0 の製品で価格による並べ替えが機能しない」
description: MDVA-37592 Adobe Commerce パッチは、共通カタログに価格ゼロが割り当てられている商品の価格による並べ替えが正しく機能しない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.0 がインストールされている場合に利用できます。 パッチ ID は MDVA-37592。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 30ac1e87-c32d-4e79-9ed9-d1861061d760
feature: B2B, Catalog Management, Categories, Orders, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# MDVA-37592：価格がゼロの製品で価格による並べ替えが機能しない

MDVA-37592 Adobe Commerce パッチは、共通カタログに価格ゼロが割り当てられている商品の価格による並べ替えが正しく機能しない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.0 がインストールされている場合に使用できます。 パッチ ID は MDVA-37592。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドアーキテクチャ 2.4.0-p1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメントタイプ） 2.3.6-2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

共有カタログに価格ゼロが割り当てられている製品の場合、価格で並べ替えても正しく機能しません。

<u> 前提条件 </u>:

B2B がインストールされています。

<u> 再現手順 </u>:

1. 共有カタログを有効にします。
1. 次の価格の 4 つの製品を作成して、カテゴリ（$50、$60、$70 および$80）に割り当てます。
1. 上記の製品で共有カタログを作成します。
1. 価格が 70 ドルの製品については、カスタム価格をゼロに設定します。
1. 次に、会社ユーザーを作成し、作成した共有カタログに割り当てます。
1. 会社アカウントを使用してログインし、製品が割り当てられているカテゴリを参照します。
1. 価格で並べ替えてみてください。

<u> 期待される結果 </u>:

価格がゼロの製品は正しく並べ替えられています。

<u> 実際の結果 </u>:

価格がゼロの商品が正しく並べ替えられていません。 代わりに、元の価格に従って並べ替えられます。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe Commerce オンプレミス：開発者向けドキュメントの [ ソフトウェアアップデートガイド/パッチを適用する ](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)。
* アドビのクラウドアーキテクチャ上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチを適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
