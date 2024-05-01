---
title: 'MDVA-34102：販売可能な数量が一致しない'
description: MDVA-34102 パッチを使用すると、Product Grid および Edit Product ページで無効になっている製品のデフォルトの在庫数がゼロになる問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.18 がインストールされている場合に利用できます。 パッチ ID は MDVA-34102。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。
exl-id: cb1d4689-c122-4afd-8597-b2627027aaf3
feature: Variables
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# MDVA-34102：販売可能な数量に一貫性がない

MDVA-34102 パッチを使用すると、Product Grid および Edit Product ページで無効になっている製品のデフォルトの在庫数がゼロになる問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.18 がインストールされています。 パッチ ID は MDVA-34102。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0-2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. ストアとストアビューを使用して 2 つの web サイトを設定します。
1. 追加のソースと在庫を作成します。
1. シンプルな製品を追加します。
   * を設定 **製品を有効にする** = *不可*.
   * 2 つのソースの割り当て **ソース アイテムの状態** = *在庫あり* 量が 0 より大きい場合（例： **既定の在庫** = *123* および **英国株** = *123*）に設定します。
1. 商品を保存します。
1. を確認します **商品販売可能数量** タブ。

<u>期待される結果</u>:

デフォルト在庫と英国在庫= *123。*

デフォルトの在庫数は、無効になっている製品に対して、管理の製品グリッドおよび製品を編集ページで正しく表示されます。

<u>実際の結果</u>:

デフォルトの在庫= *0* 英国の株価= *123。*

管理者の製品グリッドおよび製品を編集ページで、無効な製品のデフォルトの在庫数がゼロになります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
