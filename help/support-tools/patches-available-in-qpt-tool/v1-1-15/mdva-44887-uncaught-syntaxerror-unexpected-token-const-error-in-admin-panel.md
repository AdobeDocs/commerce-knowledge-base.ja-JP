---
title: 「MDVA-44887：管理パネルに「捕捉されていない構文エラー：予期しないトークンコンスト」エラーが表示される」
description: '「MDVA-44887 パッチは、管理者ユーザーがどのメニューオプションもクリックできない問題を修正します。 「Uncaught SyntaxError: Unexpected token const」エラーが管理パネルに表示されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.15 がインストールされている場合に利用できます。 パッチ ID は MDVA-44887。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。」'
exl-id: 66555e66-49d0-4f80-8f77-84ee107ab12e
feature: Admin Workspace, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# MDVA-44887：管理パネルの&#39;キャッチされていない構文エラー：予期しないトークン const&#39; エラー

管理者ユーザーがメニューオプションをクリックできない問題は、MDVA-44887 パッチで修正されています。 この *不明な SyntaxError：予期しないトークン定数です* エラーが管理パネルに表示されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.15 がインストールされています。 パッチ ID は MDVA-44887。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者ユーザーはどのメニューオプションもクリックできません。 この *不明な SyntaxError：予期しないトークン定数です* エラーが管理パネルに表示されます。

<u>再現手順</u>:

1. JS のバンドルを有効にします。
1. JS ファイルを縮小します。
1. Commerce管理パネルにログインします。

<u>期待される結果</u>:

管理者ユーザーはどのメニューオプションもクリックできません。 ブラウザーコンソールにエラーがあります： *不明な SyntaxError：予期しないトークン定数です*.

<u>実際の結果</u>:

管理者ユーザーは管理パネルにアクセスできます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
