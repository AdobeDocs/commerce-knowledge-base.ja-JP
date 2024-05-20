---
title: 「MDVA-30963：管理者製品検索フィルターが期待どおりに機能しない」
description: MDVA-30963 パッチを適用すると、Commerce Admin と Product Search filter が期待どおりに動作しない問題が解決されます。 ストア表示の範囲で上書きされた値は、**すべてのストア表示**ストア表示の範囲をフィルタリングする際にも考慮されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.8 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: bde2836e-8954-48e5-b411-08c951ec8620
feature: Admin Workspace, Products, Search
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# MDVA-30963：管理者製品検索フィルターが期待どおりに動作しない

MDVA-30963 パッチを適用すると、Commerce Admin と Product Search filter が期待どおりに動作しない問題が解決されます。 ストア表示の範囲で上書きされた値も、でフィルタリングする際に考慮されます **すべてのストア表示** ストア表示の範囲。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.8 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. を設定 **ストア** > **設定** > **カタログ** > **カタログ** > **価格** > **カタログの価格スコープ** = *Web サイト*.
1. 2 つの異なる通貨を持つ 2 つの web サイトを作成します（例えば、デフォルトの web サイトは India Store \[Rupee ₹\]、2 つ目の web サイトは US Store \[Dollar $\]）。
1. 以下を設定します **基準通貨**, **既定の表示通貨**、および **許可される通貨**:
   * **デフォルトの設定** = *米ドル （デフォルト）*
   * **メイン Web サイト** = *ルピー（インド）*
   * **WebsiteUS** = **デフォルトを使用** = *米ドル*
1. を設定 **ストア** > **通貨レート** = *1:1*.
1. 次の価格で、両方の web サイトに割り当てられたテスト用のシンプルな製品を作成します。
   * **デフォルトの価格** = **米国ウェブサイト価格** = *123 USD*
   * **メインウェブサイト価格** = *321 ルピー*
1. US ストアへのアクセス権のみを持つ subAdmin ユーザーを作成します。
1. 米国ストアフロントに移動し、商品をカートに入れます（例： *123 米ドル価格*）に設定します。
1. 先ほど作成した subAdmin で管理者にログインします（例： *US のみの管理者*）に設定します。
1. に移動 **報告書** > **カート内の製品**.

<u>期待される結果</u>:

内でフィルタリングする場合 **すべてのストア表示** ストア表示の範囲、製品フィルタリングでは、その特定の範囲で設定された値を取得する必要があります。

<u>実際の結果</u>:

「すべてのストア表示」のストア表示範囲をフィルタリングする場合、ストア表示範囲で上書きされた値も考慮されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
