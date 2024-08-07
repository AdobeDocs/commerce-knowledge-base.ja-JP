---
title: 「MDVA-36424：ページビルダーに添付された画像が保存時に消える」
description: MDVA-36424 パッチを使用すると、複数の Web サイトの場合、カテゴリを 2 回目に保存すると、ページビルダー要素に添付されている画像が消える問題を解決できます。デフォルトの Web サイトのベース URL は管理者 URL とは異なります。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.21 がインストールされている場合に利用できます。 パッチ ID は MDVA-36424。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: ae15db2d-0d9f-48c1-87e4-61da1558a57c
feature: Categories, Page Builder
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# MDVA-36424：ページビルダーに添付された画像が保存時に消える

MDVA-36424 パッチを使用すると、複数の Web サイトの場合、カテゴリを 2 回目に保存すると、ページビルダー要素に添付されている画像が消える問題を解決できます。デフォルトの Web サイトのベース URL は管理者 URL とは異なります。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.21 がインストールされている場合に使用できます。 パッチ ID は MDVA-36424。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.6

**Magentoバージョンと互換性あり：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.1-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

バックエンドのベース URL がストアフロントのベース URL と異なる場合、ページビルダー要素に添付されたメディア画像は保存されません。

<u> 再現手順 </u>:

1. 2 つ目の web サイト（website2）を作成します。
1. Web サイト 2 に別のベース URL を設定します（管理者で使用するベース URL は 2 つ目の web サイトとは異なる必要があります）。
1. 2 つ目の web サイトをデフォルトの web サイトとして設定します（**ストア**/*設定*/**すべてのストア**/2 つ目の web サイトを選択/*デフォルト*）に設定します。
1. バックエンドのカテゴリページに移動し、カテゴリ編集ビューに移動します。
1. **コンテンツ**/*説明* に移動します。
1. メディアギャラリーを使用して、コンテンツに列を追加し、背景画像を設定します。
1. カテゴリの保存。
1. **コンテンツ**/*説明* に再度移動します。保存された画像が正しく表示されます。
1. カテゴリを再度保存します。
1. **コンテンツ**/*説明* に移動します。

<u> 期待される結果 </u>:

カテゴリの保存時に画像が削除されない。

<u> 実際の結果 </u>:

カテゴリを 2 回目に保存した後で画像が削除されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
