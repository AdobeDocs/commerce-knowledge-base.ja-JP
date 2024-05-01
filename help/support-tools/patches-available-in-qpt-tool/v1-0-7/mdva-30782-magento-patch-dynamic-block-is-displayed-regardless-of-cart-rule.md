---
title: 「MDVA-30782：買い物かごのルールに関係なく、動的ブロックが表示される」
description: MDVA-30782 パッチは、買い物かごのルールに関係なく、動的ブロックが表示される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 88da8853-aae7-4fd9-82ba-a4e9fc99cf53
feature: Cache, Orders, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# MDVA-30782：買い物かごのルールに関係なく、動的ブロックが表示される

MDVA-30782 パッチは、買い物かごのルールに関係なく、動的ブロックが表示される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

関連するカタログ価格ルール条件が満たされない場合でも、動的ブロックがページ上に表示される。

<u>再現手順</u>:

1. 2 つの製品を作成します。
1. これらの製品の 1 つに対してのみ適用できるカタログ価格ルールを作成します。
1. 動的ブロックを作成し、新しく作成したカタログ価格ルールをそれに割り当てます。
1. 次のパラメーターでウィジェットを作成します。
   * タイプ = ダイナミック ブロック ロケータ
   * 表示するダイナミック ブロック =指定されたダイナミック ブロック
   * ダイナミック ブロックを指定= ブロック フォーム ステップ \#3Layout 更新（任意）
   * 表示対象=すべての製品タイプ
   * コンテナ =製品の補助情報
1. 再インデックスを実行し、キャッシュをフラッシュします。
1. 両方の製品ページでダイナミックブロックフォームステップを確認\#3

<u>期待される結果</u>:

ダイナミックブロックは最初の製品ページにのみ表示されます。

<u>実際の結果</u>:

ダイナミックブロックが両方の製品ページに表示されます。 表示する動的ブロック = ステップ\#3 のカタログ価格ルール関連を使用すると、結果は同じになります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
