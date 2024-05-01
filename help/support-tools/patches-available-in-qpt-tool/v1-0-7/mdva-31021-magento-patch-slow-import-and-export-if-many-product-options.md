---
title: 「MDVA-31021：製品オプションが多い場合、読み込みと書き出しに時間がかかる」
description: MDVA-31021 パッチは、多数の製品オプションがある場合にインポート/エクスポートに予想以上の時間がかかる場合の問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。
exl-id: d294b30d-b734-4bd6-bf1a-c116b789a63c
feature: Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# MDVA-31021：多くの製品オプションがある場合、インポートとエクスポートに時間がかかる

MDVA-31021 パッチは、多数の製品オプションがある場合にインポート/エクスポートに予想以上の時間がかかる場合の問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

に 10 万件以上のレコードがある場合 `catalog_product_option` テーブル、インポート/エクスポート関数ファイルの検証に予想以上の時間がかかります。 インポート/エクスポートの前に、オプションの検証を確認するために、Adobe Commerceは既存のすべての商品の商品オプションを読み込みます。

<u>前提条件</u>:

カスタムオプションを含む 5000 商品のAdobe Commerceストア。 に 100,000 件のレコードが存在するように、各製品には、2 つ以上のオプションから選択できる少なくとも 4 つのカスタムオプションが必要です `catalog_product_option` テーブル。

<u>再現手順</u>:

1. の場合 **インポート** 例：Commerce管理者の SKU のいずれかを使用して CSV インポートファイルを作成する
1. CSV 読み込みファイルに 4 つのカスタムオプションを追加します。
1. Commerce Admin から CSV ファイルを読み込んでみます。

<u>期待される結果</u>:

インポートまたはエクスポート機能が期待どおりに完了します。 1 つの製品で検証が完了するまで 10 秒未満です。

<u>実際の結果</u>:

インポートまたはエクスポート機能に予想以上の時間がかかります。 1 つの製品のみで検証が完了するまで 10 秒以上かかります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
