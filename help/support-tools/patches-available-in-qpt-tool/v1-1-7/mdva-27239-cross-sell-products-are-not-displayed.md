---
title: 「MDVA-27239：クロスセル製品が表示されない」
description: MDVA-27239 パッチを適用すると、クロスセル製品が表示されない問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.3.6 で修正されました。
exl-id: a0392a07-645d-4811-8547-2c67e20b6313
feature: Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# MDVA-27239：クロスセル製品が表示されない

MDVA-27239 パッチを適用すると、クロスセル製品が表示されない問題が修正されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.7 がインストールされています。 この問題はAdobe Commerce 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.4、2.4.0

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.5-p2、2.4.0 ～ 2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

クロスセル製品は、買い物かごページのクロスセルブロックには表示されません。

<u>前提条件</u>:

1. Layout_TargetRule モジュールを無効化するか、Magentoブロック Magento\TargetRule\Block\Checkout\Cart\Crosssellから削除します。
1. 製品 1 を作成します。
1. 製品 1 のスケジュール更新を作成して、新しく作成された製品が entity_id とは異なる row_id になるようにします。
1. 製品 2、製品 3 および製品 4 を作成します。
1. 製品 4 のクロスセルとして製品 3 を設定します。
1. 製品 4 を製品 2 のクロスセルとして設定します。

<u>再現手順</u>:

1. 商品 4 と商品 2 を買い物かごに追加します。
1. 買い物かごページを確認します。

<u>期待される結果</u>:

製品 3 はクロスセルブロックで表示されます。

<u>実際の結果</u>:

クロスセルブロックが空です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
