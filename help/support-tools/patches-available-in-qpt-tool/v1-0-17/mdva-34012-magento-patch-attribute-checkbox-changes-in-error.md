---
title: 「MDVA-34012 パッチ：属性チェックボックスがエラーで変更される」
description: MDVA-34012 パッチを使用すると、エラーでスケジュールを更新した後に属性のチェックボックスが変更される問題を解決できます。
exl-id: 1a8f1bea-9b6a-4984-b9f0-b2b9ceb6688f
feature: Attributes
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# MDVA-34012 パッチ：属性チェックボックスがエラーで変更される

MDVA-34012 パッチを使用すると、エラーでスケジュールを更新した後に属性のチェックボックスが変更される問題を解決できます。

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.17 がインストールされています。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.1 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. 管理者にログインし、次の場所に移動します **カタログ/製品**.
1. 簡単な製品を編集します。
1. ストア表示を特定のストア表示に変更する。
1. を使用して製品を保存 **デフォルト値を使用** 属性に対して選択されたチェックボックス（例： **製品を有効にする** 属性）。
1. クリックする **新しい更新をスケジュール** 一部の変更をスケジュールするには（例： **価格** または **特別価格** （特定のストア表示の場合）。
1. 変更が完了するまで待ちます。
1. 商品を確認してください。 チェックボックスをオフにし、特定のストア属性値を指定する必要があります。

<u>期待される結果</u>:

属性のチェックボックスは同じままで、スケジュールの更新後に期待どおりに変更されません。

<u>実際の結果</u>:

属性のチェックボックスは、スケジュールの更新後に変更されます。

## パッチの適用

個々のパッチを適用するには、Adobe Commerce製品に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
