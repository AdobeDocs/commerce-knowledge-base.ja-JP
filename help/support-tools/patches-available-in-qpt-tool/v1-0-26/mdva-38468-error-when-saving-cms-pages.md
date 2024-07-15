---
title: 「MDVA-38468:CMS ページの保存時にエラーメッセージが表示される」
description: 「MDVA-38468 Adobe Commerce パッチでは、CMS ページを保存するときに「Item with the same ID "PAGE_ID" already exists,*」というエラーメッセージが表示される問題が修正されました。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.26 がインストールされている場合に利用できます。 パッチ ID は MDVA-38468。 この問題はAdobe Commerce 2.3.6 で修正されました。'
exl-id: 7fe80308-50b7-4786-a43c-cce607eb606c
feature: CMS, Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# MDVA-38468:CMS ページの保存時にエラーメッセージが表示される

MDVA-38468 Adobe Commerce パッチでは、CMS ページの保存時に「*Item with the same ID &quot;PAGE_ID&quot; already exists,* というエラーメッセージが表示される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp)1.0.26 がインストールされている場合に使用できます。 パッチ ID は MDVA-38468。 この問題はAdobe Commerce 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー 2.3.2-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.2-2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CMS ページを保存しようとすると、次のエラーメッセージが表示されます。*同じ ID を持つ項目「PAGE_ID」が既に存在します。*

<u> 再現手順 </u>:

1. 新しい Web サイト + ストア + ストアレビューを作成します。
1. Web サイト + ストア + ストアレビューをもう 1 つ作成します。
1. **コンテンツ**/**階層**/既存の CMS ページを階層ツリーに追加に移動します。
1. **コンテンツ**/**ページ**/**新しいページを追加** に移動します。
   * 任意のタイトルを追加します。
   * 「Web サイトのページ」セクションで、作成した両方のストレビューに割り当てます。
   * 「階層」セクションで、を任意のカテゴリに割り当てます。
   * **保存して編集を続行**。

<u> 期待される結果 </u>:

ページはエラーなしで保存されます。

<u> 実際の結果 </u>:

ページは保存されますが、次のエラーメッセージが表示されます。*同じ ID を持つ項目（Magento\VersionsCms\Model\Hierarchy\Node）「PAGE_ID」が既に存在します。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT ツールで使用可能なその他のパッチについては、[QPT ツールで使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
