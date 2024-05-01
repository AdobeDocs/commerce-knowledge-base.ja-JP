---
title: 「MDVA-42689：読み込み中に製品カテゴリを更新すると、整合性制約違反エラーが発生する」
description: MDVA-42689 パッチを使用すると、インポート中に製品カテゴリを更新する際に、整合性制約違反エラーが発生する問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-42689。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 7beff3bb-9313-43dc-be96-e33eff52a38e
feature: Categories, Data Import/Export, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# MDVA-42689：読み込み中に製品カテゴリを更新すると、整合性制約違反エラーが発生する

MDVA-42689 パッチを使用すると、インポート中に製品カテゴリを更新する際に、整合性制約違反エラーが発生する問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-42689。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

読み込み中に商品カテゴリの更新中に、Adobe Commerceが整合性制約違反エラーをスローする。

<u>再現手順</u>:

1. 2 つの web サイトを設定します。
1. カテゴリページのルートカテゴリの下に、最大 2 レベルのサブカテゴリを作成します。 例えば、ルートカテゴリ > **歯車** > **ウォッチ**.
1. 2 つのシンプルな製品を作成し、両方の製品を同じ製品に割り当てます **歯車** > **ウォッチ** カテゴリ。
1. 両方の web サイトに 1 つのシンプルな製品を割り当てます。
1. 商品を保存します。
1. 読み込む CSV ファイルを準備します。 異なるストア表示を持つ 2 つの製品レコードがあるはずです。 一方の製品がこれらの両方のストア表示に属している必要があります。
1. 次に移動して、CSV ファイルを読み込みます。 **システム** > **インポート** > **エンティティタイプ** （製品）。

<u>期待される結果</u>:

エラーなしで CSV ファイルが読み込まれます。

<u>実際の結果</u>:

Adobe Commerceが次のエラーをスローする：

```SQL
SQLSTATE[23000]: Integrity constraint violation: 1062 Duplicate entry '1302' for key 'PRIMARY', query was: INSERT INTO `catalog_url_rewrite_product_category` (`url_rewrite_id`,`category_id`,`product_id`) VALUES (?, ?, ?), (?, ?, ?), (?, ?, ?)
```

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
