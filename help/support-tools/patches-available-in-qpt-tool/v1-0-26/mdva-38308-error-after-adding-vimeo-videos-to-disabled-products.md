---
title: 「MDVA-38308：無効な製品に Vimeo ビデオを追加した後にエラーが発生する」
description: '「Adobe Commerce用 MDVA-38308 品質パッチを適用すると、Vimeo ビデオを無効な商品に追加する際に、/lib/internal/Magento/Framework/File/Uploader.phpで「Notice: Undefined index: extension in on line 806,*」というエラーメッセージが表示される問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.26 がインストールされている場合に利用できます。 パッチ ID は MDVA-38308。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。'''
exl-id: ed5fb9ec-c465-4bb9-8a29-4d5e4bd4c867
feature: Products
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# MDVA-38308：無効な製品に Vimeo ビデオを追加した後にエラーが発生する

Adobe Commerce用の MDVA-38308 品質パッチは、次のエラーメッセージが表示される問題を解決します。 *注意：未定義のインデックス：/lib/internal/Magento/Framework/File/Uploader.phpの 806 行目の拡張子* 無効にした製品に Vimeo 動画を追加する場合。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.26 がインストールされています。 パッチ ID は MDVA-38308。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー上のAdobe Commerce 2.4.1-p1、2.4.2-p1

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.5 - 2.3.6-p1、2.4.0 - 2.4.1-p1、2.4.2 - 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

無効にした製品に Vimeo 動画を追加すると、次のエラーメッセージが表示されます。  *注意：未定義のインデックス：/lib/internal/Magento/Framework/File/Uploader.phpの 806 行目の拡張子*

<u>再現手順</u>:

1. シンプルな製品を作成します。
1. 作成した製品を無効にします。
1. 無効にした製品に Vimeo ビデオを追加してみてください。

<u>期待される結果</u>:

ビデオがエラーなしで追加されます。

<u>実際の結果</u>:

次のエラーが発生します。
*注意：未定義のインデックス：/lib/internal/Magento/Framework/File/Uploader.phpの 806 行目の拡張子*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe Commerce オンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html)

## 関連資料

サポートナレッジベースの品質向上パッチツールについて詳しくは、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節（サポートナレッジベース）を参照してください。
