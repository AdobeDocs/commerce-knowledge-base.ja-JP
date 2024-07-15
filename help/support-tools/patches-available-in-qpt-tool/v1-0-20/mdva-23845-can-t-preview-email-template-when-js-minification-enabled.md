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

このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.20 がインストールされている場合に使用できます。 パッチ ID は MDVA-23845。 この問題は、Magentoバージョン 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Magentoバージョン用のパッチが作成されます。** Magento Commerce Cloud 2.3.3

**Magento版との互換性：** Magento Commerceおよび Magneto Commerce Cloud 2.3.2-2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u> 再現手順 </u> :

1. **管理/ストア/設定/JavaScript設定/JavaScript ファイルを縮小** で **JS の縮小を有効にします** = *はい*。
1. Magentoを実稼動モードに切り替えます。
1. **管理者/マーケティング/コミュニケーション/電子メールテンプレート** に移動します。
1. 「**新しいテンプレートを追加**」をクリックします。
1. **新規注文** テンプレートを選択します。
1. 「**テンプレートを読み込み**」ボタンをクリックします。
1. **テンプレート名** に **新規注文** を入力します。
1. 「**テンプレートを保存**」ボタンをクリックします。
1. メールテンプレートグリッドで、「**アクション** 列の **プレビュー** リンクをクリックします。

<u> 期待される結果 </u> :

開いたポップアップウィンドウに、メールテンプレートのプレビューが期待どおりに表示されます。

<u> 実際の結果 </u> :

開いたポップアップウィンドウに、メールテンプレートのプレビューが表示されません。 ポップアップウィンドウは空で、JS エラーが表示される場合があります。

## パッチの適用

個別のパッチを適用するには、Magentoに応じて次のリンクを使用します。

* Magento Commerce: DevDocs [ ソフトウェアアップデートガイド/パッチを適用 ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html)。
* Magento Commerce Cloud: DevDocs[ アップグレードとパッチ/パッチを適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで適用する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool でパッチのMagentoの問題を確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
