---
title: 「MDVA-44100：すべての FPT が買い物かごの最後の製品に割り当てられる」
description: MDVA-44100 パッチを適用すると、買い物かごの最後の製品にすべての FPT が割り当てられる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-44100。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: ab0f195c-fcc6-41ac-932d-d2603d068aa6
feature: Orders, Products, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# MDVA-44100：すべての FPT が買い物かごの最後の製品に割り当てられる

MDVA-44100 パッチを適用すると、買い物かごの最後の製品にすべての FPT が割り当てられる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.14 がインストールされている場合に使用できます。 パッチ ID は MDVA-44100。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

すべての FPT が買い物かごの最後の製品に割り当てられ、残りの製品の FPT 値はリセットされます。

<u> 再現手順 </u>:

1. **Stores**/**Configuration**/**Sales**/**Tax** に移動し、次のように設定します。
   * FPT を有効にする= Yes
   * FPT への税金の適用= Yes
   * 小計に FPT を含める=はい
1. **ストア**/**属性**/**製品** に移動し、type = Fixed Product Tax という新しい属性を作成します。
1. 属性セットに属性を追加します。
1. 属性セットから 2 つの製品を作成し、国と州の FPT 属性を設定します。
1. 両方の品目を受注に追加します。
1. FPT の支払いが必要な住所を入力します。
1. 注文します。
1. 注文の品目リストを確認します。

<u> 期待される結果 </u>:

FPT は各製品の下に表示されます。

<u> 実際の結果 </u>:

両方の項目の FPT 値が 2 番目の項目の下に表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
