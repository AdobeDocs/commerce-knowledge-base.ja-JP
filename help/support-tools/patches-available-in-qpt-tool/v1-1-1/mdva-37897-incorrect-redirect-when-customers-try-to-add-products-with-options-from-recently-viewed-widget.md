---
title: 「MDVA-37897：最近表示された項目から製品を追加する際に、リダイレクトが正しく表示されない」
description: MDVA-37897 パッチを使用すると、最近表示された項目ウィジェットからオプションを含む製品を追加しようとすると、誤ったリダイレクトの問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.1 がインストールされている場合に利用できます。 パッチ ID は MDVA-37897。 この問題はAdobe Commerce バージョン 2.4.4 で修正される予定であることに注意してください。
exl-id: f0a86e02-b357-4d2d-8386-e9cc045bcf06
feature: Products
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# MDVA-37897：最近表示された項目から製品を追加すると、リダイレクトが正しく表示されない

MDVA-37897 パッチを使用すると、最近表示された項目ウィジェットからオプションを含む製品を追加しようとすると、誤ったリダイレクトの問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.1 がインストールされている場合に使用できます。 パッチ ID は MDVA-37897。 この問題はAdobe Commerce バージョン 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャ 2.4.1 のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ユーザーが「最近閲覧された項目」セクションから選択の必要なオプションを含む製品を追加しようとすると、ユーザーは製品の詳細ページではなく製品一覧ページにリダイレクトされます。

<u> 再現手順 </u>:

1. カスタマイズ可能なオプション（タイプ：ラジオボタン）を使用して、シンプルな製品を作成します。
1. 最近表示された項目ウィジェットを設定して、製品を表示します。
1. 最近表示されたウィジェットに表示されるように、カスタマイズ可能なオプションを持つ製品を訪問します。
1. 最近表示されたウィジェットのいずれかの製品で、「**買い物かごに追加**」をクリックします。

<u> 期待される結果 </u>:

製品の詳細ページにリダイレクトされて、オプションを選択できます。

<u> 実際の結果 </u>:

製品一覧ページにリダイレクトされます。

## パッチの適用

個々のパッチを適用するには、デプロイメントタイプに応じて次のリンクを使用します。

* Adobe Commerce オンプレミス：開発者向けドキュメントの [ ソフトウェアアップデートガイド/パッチを適用する ](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)。
* アドビのクラウドインフラストラクチャでのAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチを適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

Adobe Commerce用の高品質パッチの詳細については、次を参照してください。

* [ 品質パッチツールがリリースされました：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で使用可能なその他のパッチについては、[QPT で使用可能なパッチ ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節を参照してください。
