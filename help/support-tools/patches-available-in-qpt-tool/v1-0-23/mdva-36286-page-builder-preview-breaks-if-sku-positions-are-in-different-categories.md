---
title: 「MDVA-36286：異なるカテゴリの SKU が位置する場合にページビルダーのプレビューが機能しない」
description: MDVA-36286 パッチでは、同じ SKU のサブカテゴリ内で位置が異なる場合に、ページビルダー製品のウィジェットプレビューが機能しなくなる問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.23 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 0f7d2506-569a-4b70-82bf-0f153014c48a
feature: CMS, Categories, Page Builder
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# MDVA-36286:SKU が異なるカテゴリに配置されている場合にページビルダーのプレビューが機能しない

MDVA-36286 パッチでは、同じ SKU のサブカテゴリ内で位置が異なる場合に、ページビルダー製品のウィジェットプレビューが機能しなくなる問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.23 がインストールされています。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.6

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.6 - 2.4.2-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順：</u>

1. いくつかの製品でカテゴリを作成します。
   ![products_magento_ordered.png](/help/support-tools/patches-available-in-qpt-tool/assets/products_magento_ordered.png)
1. 同じ商品を使用し、位置が異なるサブカテゴリを作成します。
   ![products_magento_different_position.png](/help/support-tools/patches-available-in-qpt-tool/assets/products_magento_different_position.png)
1. CMS ページのコンテンツを編集し、ページビルダーを使用して製品ウィジェットを追加します。 （上で親カテゴリを選択してください）。
   ![cms_page_magento.png](/help/support-tools/patches-available-in-qpt-tool/assets/cms_page_magento.png)
1. 保存して、コンテンツのプレビューを待ちます。

<u>期待される結果：</u>

コンテンツのプレビューには、製品ウィジェットが表示されます。

<u>実際の結果：</u>

次のエラーが表示されます。

*申し訳ありませんが、このコンテンツの生成中にエラーが発生しました。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
