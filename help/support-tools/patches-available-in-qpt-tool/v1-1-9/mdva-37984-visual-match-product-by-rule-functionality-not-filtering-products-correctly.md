---
title: 「MDVA-37984：ステージングの更新が適用されている場合、ビジュアルマーチャンダイザーが正しく機能しない」
description: MDVA-37984 パッチを使用すると、ステージングアップデートが適用される際に、ビジュアルマーチャンダイザーの「製品をルールで一致させる」機能で製品が正しくフィルタリングされない問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.9 がインストールされている場合に利用できます。 パッチ ID は MDVA-37984。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: d806b94c-3b22-4d4c-8afb-7b57a0ebfe46
feature: Categories, Merchandising, Products, Staging
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# MDVA-37984：ステージング更新が適用されている場合、ビジュアルマーチャンダイザーが正しく機能しない

MDVA-37984 パッチを使用すると、ステージングアップデートが適用される際に、ビジュアルマーチャンダイザーの「製品をルールで一致させる」機能で製品が正しくフィルタリングされない問題が解決されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.9 がインストールされています。 パッチ ID は MDVA-37984。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ステージングアップデートが適用される場合、ビジュアルマーチャンダイザーの「ルールで製品を一致させる」機能で、製品が正しくフィルタリングされません。

<u>再現手順</u>:

1. 既存の製品のスケジュール更新を作成します。
   * 別の値を設定： `entity_id` および `row_id`.
1. 設定可能な新しい製品を作成し、シンプルな製品（新しい製品）を作成します `entity_id` および `row_ids` も異なります）。
   * 問題の再現を容易にするには、シンプルな製品に識別可能な数量の値（例：5000）を設定します。
1. カテゴリに移動 > **カテゴリ内の製品** および有効化 **ルールで製品を照合**.
1. 次に、属性として「数量」、演算子として「より大きい」、値として「4500」を選択します。
1. クリック **保存**.

<u>期待される結果</u>:

新しく作成された設定可能なプロダクトがリストされます。

<u>実際の結果</u>:

新しく作成された設定可能なプロダクトはリストされません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
