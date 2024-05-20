---
title: 「MDVA-38468:CMS ページの保存時にエラーメッセージが表示される」
description: 「MDVA-38468 Adobe Commerce パッチでは、CMS ページを保存するときに「Item with the same ID "PAGE_ID" already exists,*」というエラーメッセージが表示される問題が修正されました。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.26 がインストールされている場合に利用できます。 パッチ ID は MDVA-38468。 この問題はAdobe Commerce 2.3.6 で修正されました。'
exl-id: 7fe80308-50b7-4786-a43c-cce607eb606c
feature: CMS, Categories
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# MDVA-38468:CMS ページの保存時にエラーメッセージが表示される

MDVA-38468 Adobe Commerce パッチでは、次のエラーメッセージが表示される問題が修正されています。 *同じ ID を持つ項目「PAGE_ID」が既に存在しています。* cms ページの保存時。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.26 がインストールされています。 パッチ ID は MDVA-38468。 この問題はAdobe Commerce 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー 2.3.2-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.2-2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CMS ページを保存しようとすると、次のエラーメッセージが表示されます。 *同じ ID 「PAGE_ID」の項目が既に存在しています。*

<u>再現手順</u>:

1. 新しい Web サイト + ストア + ストアレビューを作成します。
1. Web サイト + ストア + ストアレビューをもう 1 つ作成します。
1. に移動 **コンテンツ** > **階層** > 階層ツリーに既存の CMS ページを追加します。
1. に移動 **コンテンツ** > **ページ** > **新しいページを追加**:
   * 任意のタイトルを追加します。
   * 「Web サイトのページ」セクションで、作成した両方のストレビューに割り当てます。
   * 「階層」セクションで、を任意のカテゴリに割り当てます。
   * **保存して編集を続行**.

<u>期待される結果</u>:

ページはエラーなしで保存されます。

<u>実際の結果</u>:

ページは保存されますが、次のエラーメッセージが表示されます。 *同じ ID 「PAGE_ID」の項目（Magento\VersionsCms\Model\Hierarchy\Node）が既に存在しています。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
