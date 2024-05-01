---
title: 「ACSD-45520：製品の詳細ページでスウォッチオプションが選択されない」
description: ACSD-45520 パッチは、ユーザーが買い物かごから設定可能な製品を編集する際に、製品の詳細ページでスウォッチオプションが事前に選択されていない問題を修正しています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45520 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 941f4a45-bc3c-44c0-a582-ddfe179fa8c3
feature: Products
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# ACSD-45520：製品の詳細ページでスウォッチオプションが選択されない

ACSD-45520 パッチは、ユーザーが買い物かごから設定可能な製品を編集する際に、製品の詳細ページでスウォッチオプションが事前に選択されていない問題を修正しています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.17 がインストールされています。 パッチ ID は ACSD-45520 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーが買い物かごから設定可能な製品を編集すると、製品の詳細ページでスウォッチオプションが選択されません。

<u>再現手順</u>:

1. 商品オプション（色など）を使用して設定可能な商品を作成します。
1. 設定可能な製品を買い物かごに追加します。
1. 自分の買い物かごページに移動します。
1. 手順 1 で追加した設定可能な製品の「編集」ボタンをクリックします。
1. 編集ページの製品オプションを確認します。

<u>期待される結果</u>:

製品オプションが選択されます。

<u>実際の結果</u>:

製品オプションが選択されていません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
