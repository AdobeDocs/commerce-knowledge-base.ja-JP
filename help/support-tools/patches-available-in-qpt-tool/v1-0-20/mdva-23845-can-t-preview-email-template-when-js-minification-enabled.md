---
title: 「MDVA-23845:JS の縮小が有効な場合、メールテンプレートをプレビューできない」
description: JS の縮小が有効になっている場合に、管理者でメールテンプレートをプレビューできない場合の、MDVA-23845 Magentoパッチの問題が修正されました。
exl-id: 08579251-a0aa-4e84-9d6a-3fa2999d9c05
feature: Communications, Marketing Tools
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# MDVA-23845:JS の縮小が有効な場合、メールテンプレートをプレビューできない

JS の縮小が有効になっている場合に、管理者でメールテンプレートをプレビューできない場合の、MDVA-23845 Magentoパッチの問題が修正されました。

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.20 がインストールされています。 パッチ ID は MDVA-23845。 この問題は、Magentoバージョン 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Magentoバージョン用のパッチが作成されます。** Magento Commerce Cloud 2.3.3

**Magentoバージョンとの互換性：** Magento Commerceと MagnetoCommerce Cloud2.3.2-2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u> :

1. Enable （有効） **JS の縮小** 。対象： **管理者/ ストア /設定/ JavaScript 設定/ JavaScript ファイルを縮小** = *はい* .
1. Magentoを実稼動モードに切り替えます。
1. に移動 **管理者/ マーケティング /通信/電子メールテンプレート** .
1. クリック **新規テンプレートを追加** .
1. 「」を選択します **新しい注文** テンプレート。
1. 「」をクリックします **テンプレートの読み込み** ボタン。
1. 満タンにする **テンプレート名** （を使用） **新しい注文。**
1. 「」をクリックします **テンプレートの保存** ボタン。
1. メールテンプレートグリッドで、 **プレビュー** 内のリンク **アクション** 列。

<u>期待される結果</u> :

開いたポップアップウィンドウに、メールテンプレートのプレビューが期待どおりに表示されます。

<u>実際の結果</u> :

開いたポップアップウィンドウに、メールテンプレートのプレビューが表示されません。 ポップアップウィンドウは空で、JS エラーが表示される場合があります。

## パッチの適用

個別のパッチを適用するには、Magentoに応じて次のリンクを使用します。

* Magento Commerce:DevDocs [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html) .
* Magento Commerce Cloud:DevDocs [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) .

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) .
* [Quality Patches Tool を使用して、Magentoの問題に対するパッチをチェックします。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) .

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
