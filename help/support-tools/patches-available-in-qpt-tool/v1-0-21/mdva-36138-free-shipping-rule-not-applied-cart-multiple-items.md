---
title: 「MDVA-36138：送料無料ルールが買い物かごに複数の項目を適用しない」
description: MDVA-36138 パッチでは、カートに複数のアイテムが入っている場合、送料無料で一致する SKU に送料無料が適用されない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.21 がインストールされている場合に利用できます。 パッチ ID は MDVA-36138。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: 74e25ca8-e4fa-47f4-ab95-561f70e05727
feature: Orders, Shipping/Delivery, Personalization, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# MDVA-36138：送料無料ルールがカートに複数のアイテムを適用しない

MDVA-36138 パッチでは、カートに複数のアイテムが入っている場合、送料無料で一致する SKU に送料無料が適用されない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.21 がインストールされています。 パッチ ID は MDVA-36138。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.4

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.2 以降

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

特定の商品のみに送料無料ルールが適用される場合、カートに他の商品がある場合、割引は適用されません。

<u>再現手順</u>:

1. シンプルな製品 – simple1 と simple2 を作成します。
1. USPS （または任意のオンライン配送方法）を設定します。

   * 許可されるメソッド：優先メール （買い物かごおよびチェックアウトに長いメソッドのリストを持たないという目的で選択された 1 つのメソッド）。
   * フリーメソッド：優先メール。

1. 買い物かごルールを作成します。

   * クーポンコードを指定
   * 「条件」タブ：空のままにします
   * 「アクション」タブ：

   `Condition: SKU is simple1`
   `Free Shipping: For matching items only`

1. simple1 をカートに追加します。
1. クーポンコードを適用します。
1. simple2 を買い物かごに追加します。

<u>期待される結果</u>:

* simple1 – 送料無料にする必要があります。
* simple2 – 送料を支払う必要があります。

<u>実際の結果</u>:

送料には simple1 と simple2 が含まれます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
