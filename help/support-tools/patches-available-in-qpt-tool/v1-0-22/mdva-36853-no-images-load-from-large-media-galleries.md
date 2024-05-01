---
title: 「MDVA-36853：大規模なメディアギャラリーから画像が読み込まれない」
description: 大きなメディアディレクトリがある場合、ページビルダーのメディアギャラリーウィジェットが読み込まれないので、画像が読み込まれない場合の MDVA-36853 パッチの問題を修正しました。
exl-id: 64e089d9-d443-4aa7-8e04-a3598b05958d
feature: CMS, Cache, Media
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# MDVA-36853：大きなメディアギャラリーから画像が読み込まれない

大きなメディアディレクトリがある場合、ページビルダーのメディアギャラリーウィジェットが読み込まれないので、画像が読み込まれない場合の MDVA-36853 パッチの問題を修正しました。

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.22 がインストールされています。 パッチ ID は MDVA-36853。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. を設定 **古いメディアギャラリーを有効にする** = *はい* 。対象： **管理者/ ストア /設定/詳細/ システム / メディアギャラリー**.
1. に移動します。 **コンテンツ/ブロック**&#x200B;を選択して、新しい CMS ブロックを作成するか、既存の CMS ブロックを編集します。
1. 「」をクリック **Pagebuilder で編集** ボタン。
1. メディア要素を追加します。
1. 「」をクリック **ギャラリーから選択** ボタン。

<u>期待される結果</u>:

メディアギャラリーウィジェットとメディアギャラリー画像の両方が、期待どおりに読み込まれます。

<u>実際の結果</u>:

サイズが大きい場合、メディアギャラリーウィジェットとメディアギャラリー画像の両方が読み込まれません `pub/media/catalog/product/cache/` ディレクトリ。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
