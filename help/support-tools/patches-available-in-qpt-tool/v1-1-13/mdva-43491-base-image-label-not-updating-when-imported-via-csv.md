---
title: 「MDVA-43491:CSV 経由で読み込むと、ベース画像ラベルが更新されない」
description: MDVA-43491 パッチでは、マルチストア web サイトの CSV ファイルを使用して読み込んだ場合に「base_image_label」が更新されない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.13 がインストールされている場合に利用できます。 パッチ ID は MDVA-43491。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: d744423a-f582-4410-8d66-861229cce1b5
feature: Data Import/Export
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# MDVA-43491:CSV 経由で読み込むと、ベース画像ラベルが更新されない

MDVA-43491 パッチにより、 `base_image_label` マルチストア web サイトの CSV ファイルを使用して読み込んだ場合、は更新されません。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.13 がインストールされています。 パッチ ID は MDVA-43491。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この `base_image_label` マルチストア web サイトの CSV ファイルを使用して読み込んだ場合、は更新されません。

<u>前提条件</u>:

1 つ以上の既存のデフォルト以外の web サイト、ストア、ストアビュー。

<u>再現手順</u>:

1. 新しい製品を作成します。

   * 画像をアップロードします。
   * 新しく作成した web サイトに製品を割り当てます。

1. 製品を CSV として書き出します。
1. を更新 `base_image_label` 各ストア表示で、CSV ファイルのデフォルト行を複製します。
1. CSV ファイルを読み込みます。 各ストアのラベルを正しく更新します。これは、 **画像とビデオ** 製品の編集ページの「」タブ。
1. CSV ファイルを再度エクスポートして、 `base_image_label` 異なる値を持つ列。
1. CSV ファイルを再度読み込みます。
1. 管理で製品を開き、ストア表示ごとにラベルが更新されているかどうかを確認します。

<u>期待される結果</u>:

代替テキスト（画像ラベル）が、CSV ファイルに従って、ストア固有の値で更新されます。

<u>実際の結果</u>:

代替テキスト（画像ラベル）が `base_image_label` csv ファイル内の値。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
