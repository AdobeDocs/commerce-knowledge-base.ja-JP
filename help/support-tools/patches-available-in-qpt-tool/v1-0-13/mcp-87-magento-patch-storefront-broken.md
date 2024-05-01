---
title: 'MCP-87 Adobe Commerce パッチ：ストアフロントが破損'
description: MCP-87 Adobe Commerce パッチでは、カタログの在庫インデックス再作成が遅くなる問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.13 がインストールされている場合に利用できます。
exl-id: 048b2764-6bbf-4a02-9a0a-dbea4e48f92a
feature: Storefront
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# MCP-87Adobe Commerceパッチ：ストアフロントが破損している

MCP-87 Adobe Commerce パッチでは、カタログの在庫インデックス再作成が遅くなる問題を修正しました。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.13 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.1 ～ 2.4.1。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

大きなプロファイルを含むカタログのインデックス再作成が非常に遅い。

<u>再現手順：</u>

1. 管理パネルにログインします。
1. 次の場所に移動します。 **製品** > **カタログ**.
1. 製品グリッドのすべての項目を選択します。
1. を選択 **属性を更新** 「製品アクションを選択」ドロップダウンリストで選択します。 クリック **Submit**.
1. クリックする **詳細在庫** 「詳細設定」タブから変更します。 変更 **在庫状況** 対象： *在庫あり*. クリック **保存**.
1. 手動で完全な再インデックスを実行し、ルートから次のコマンドを実行します。 `bin/magento indexer:reindex`

<u>期待される結果：</u>

Stock インデクサーは迅速にインデックスを再作成します。

<u>実際の結果：</u>

Stock インデクサーが非常に遅い、または完了しない。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
