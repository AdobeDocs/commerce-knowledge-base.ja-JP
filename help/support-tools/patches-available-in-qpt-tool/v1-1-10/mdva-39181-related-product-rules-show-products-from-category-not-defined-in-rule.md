---
title: 「MDVA-39181：関連製品ルールで、ルールで定義されていないカテゴリの製品が表示される」
description: MDVA-39181 パッチを使用すると、関連する製品ルールに定義されていないカテゴリの製品が表示される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.10 がインストールされている場合に利用できます。 パッチ ID は MDVA-39181。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: b6364d1c-2480-483a-9a83-ac91feeb14b9
feature: Categories, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# MDVA-39181：関連製品ルールで、ルールに定義されていないカテゴリの製品が表示される

MDVA-39181 パッチを使用すると、関連する製品ルールに定義されていないカテゴリの製品が表示される問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.10 がインストールされている場合に使用できます。 パッチ ID は MDVA-39181。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

関連する製品ルールには、ルールで定義されていないカテゴリの製品が表示されます。

<u> 前提条件 </u>:

サンプルデータをインストールします。

<u> 再現手順 </u>:

1. 属性ブランドを作成して、**Tops 属性セット** に追加します。
1. **Josie**、**Augusta**、**Ingrid** の各ジャケットを選択し、**Women**/**Tops**/**Jackets category** からブランドキティに追加します。
1. **Men**/**Tops**/**Jacket category** からブランドのキティに追加するジャケットは、**Beaumont**、**Hyperion**、**Kenobi** を選択してください。
1. 関連製品を次のように作成します。

   ```markdown
   Apply To: Related Products
   Customer Segments: All
   ```

   * 一致する製品：

   ```markdown
   If ALL of these conditions are TRUE
     Category is {}
     Brand is {}
   ```

   * 表示する製品：

   ```markdown
   If ALL of these conditions are TRUE
      Product Category is the same as Matched Product Category
      Product brand is Matched Product Brand
   ```

1. フロントエンドから SKU WJ04 を開き、関連製品を確認します。
1. カテゴリ ID が次と異なる場合は、**Women**/**Tops**/**Jackets** からカテゴリ ID を更新します。

<u> 期待される結果 </u>:

関連製品には、同じブランドおよび同じ子カテゴリの製品のみが表示されます。

<u> 実際の結果 </u>:

関連製品は、同じブランドで、ランダムな親カテゴリから表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
