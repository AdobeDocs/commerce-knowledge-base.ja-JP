---
title: 「MDVA-31343 パッチ：スケジュール更新でカテゴリの本文クラスが削除される」
description: MDVA-31343 パッチは、スケジュールされた更新中に、カテゴリに割り当てられたレイアウト本文の CSS クラスが削除される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正される予定です。
exl-id: 50dbff01-cb77-4cac-b90e-5c4b06f5e4e7
feature: Cache, Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# MDVA-31343 パッチ：スケジュール更新でカテゴリの本文クラスが削除される

MDVA-31343 パッチは、スケジュールされた更新中に、カテゴリに割り当てられたレイアウト本文の CSS クラスが削除される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正される予定です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.4 - 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

スケジュールされた更新後、レイアウト本文クラスがカテゴリから削除されます。

<u>再現手順</u>:

1. Commerce Admin で、カテゴリを作成します。
1. を設定 **レイアウト** = *Category — Full width* が含まれる **デザイン** セクション。
1. カテゴリの保存。
1. カテゴリフロントエンドページに移動します。 ページソースに、

   ```css
   page-layout-category-full-width
   ```

   CSS クラス。
1. 次の下 **カタログ** > **カテゴリ**&#x200B;を選択し、 **新しい更新をスケジュール** が含まれる *スケジュールされた変更* 新しいカテゴリの「」セクション
1. スケジュールされた更新が開始されるのを待ち、cron を実行してキャッシュをフラッシュします。
1. フロントエンドのカテゴリページに移動し、ページソースを調べます。

<u>期待される結果</u>:

ページ本文には、

```css
page-layout-category-full-width
```

CSS クラス。

<u>実際の結果</u>:

ページ本文には、

```css
page-layout-2columns-left
```

CSS クラス（カテゴリページのデフォルト）。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
