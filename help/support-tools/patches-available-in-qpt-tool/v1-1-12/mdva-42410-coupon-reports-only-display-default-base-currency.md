---
title: 「MDVA-42410：クーポンレポートにはデフォルトの基本通貨のみが表示される」
description: MDVA-42410 パッチは、クーポンレポートに基本通貨のみが表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-42410。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: b442a2ce-1bd4-4f09-95fd-2c626e32f509
feature: Orders
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# MDVA-42410: クーポン レポートには既定の基本通貨のみが表示されます

MDVA-42410 パッチは、クーポンレポートに基本通貨のみが表示される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-42410。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クーポンレポートには、デフォルトの基本通貨のみが表示されます。

<u>再現手順</u>:

1. 追加の web サイト、ストア、ストア表示を作成します。
1. この新しい Web サイトに別の通貨を設定します。 例えば、ユーロです。
1. に移動 **ストア** > **通貨レート** および通貨レートの設定 **ユーロ**.
1. を作成 **買い物かご価格ルール** 特定のクーポンを使用 –  **テスト**.
1. フロントエンドに移動し、 **テスト** 新しいウェブサイトのクーポン。
1. に移動 **報告書** > **売上** > **クーポン**.
1. 範囲ドロップダウンで新しい web サイトを選択します。
1. 統計を更新し、レポートを実行します。

<u>期待される結果</u>:

クーポンレポートでは、新しい web サイトの通貨がユーロとして表示されます。

<u>実際の結果</u>:

新しい web サイトのクーポンレポートでは、デフォルトの基本通貨（この場合は USD）が使用されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
