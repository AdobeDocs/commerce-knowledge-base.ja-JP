---
title: 「MDVA-43232：ビジュアルマーチャンダイザーで商品を特別価格で上（または下）に並べ替えるとエラーが発生する」
description: MDVA-43232 パッチは、ビジュアルマーチャンダイザーの製品を特別価格で上（または下）に並べ替えると、カテゴリの保存中にエラーが発生する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-43232。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: e958a219-5e93-4ae4-94cb-f478f82ad060
feature: Categories, Merchandising, Orders, Personalization, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# MDVA-43232：ビジュアルマーチャンダイザーで商品を特別価格で上（または下）に並べ替えるとエラーが発生する

MDVA-43232 パッチは、ビジュアルマーチャンダイザーの製品を特別価格で上（または下）に並べ替えると、カテゴリの保存中にエラーが発生する問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-43232。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4 - 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ビジュアルマーチャンダイザーで製品を特別価格から上（または下）に並べ替えると、カテゴリの保存中にエラーが発生します。

<u>再現手順</u>:

1. 2 つの web サイトがあることを確認します。
1. に移動します。 **ストア** > **設定** > **カタログ** > **価格** そして、Catalog Price Scope = Website と設定します。
1. 再度、に移動します。 **ストア** > **設定** > **カタログ** > **ビジュアルマーチャンダイザー** > **カテゴリルールに表示される属性** > と特別価格を追加します。
1. シンプルな製品を作成して、両方の web サイトに製品を割り当てます。
1. 商品のデフォルトの範囲に特別価格を追加します。
1. 他の店舗のスコープに切り替え、その商品の価格と特別価格の両方を上書きします。
1. 実行 `catalog_product_price` 再インデックス。
1. に移動 **カタログ** > **カテゴリ** 新しいカテゴリを作成します。
1. カテゴリ ルールを追加して、特別価格のある製品をフィルターします。
1. カテゴリの保存。
1. 「カテゴリの製品」セクションで、「並べ替え順=特別価格」を「上（または下）」に設定します。
1. カテゴリを再度保存します。

<u>期待される結果</u>:

カテゴリはエラーなしで保存されます。

<u>実際の結果</u>:

例外がスローされます。

```php
[2022-02-07T05:58:46.297621+00:00] report.CRITICAL: Exception: Item (Magento\Catalog\Model\Product\Interceptor) with the same ID "1" already exists. in /lib/internal/Magento/Framework/Data/Collection.php:407
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
