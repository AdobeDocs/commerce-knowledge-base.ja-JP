---
title: 「MDVA-29787：関連製品が表示されない」
description: MDVA-29787 パッチを使用すると、**関連製品**がAdobe Commerce ストアのフロントエンドに表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-29787。
exl-id: ee060d7b-3b0e-4bd5-84e6-fbd6d2fa532f
feature: Cache, Marketing Tools, Products
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# MDVA-29787：関連製品が表示されない

MDVA-29787 パッチを使用すると、**関連製品** がAdobe Commerce ストアのフロントエンドに表示されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.6 がインストールされている場合に使用できます。 パッチ ID は MDVA-29787。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3.

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.0。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Commerce管理で **表示する商品** に「*次のいずれか*」条件が使用されている場合、**関連商品** のターゲットルールは機能しません。

>[!NOTE]
>
>メモ：このパッチでは、既存のターゲットルールは修正されません。 既存のターゲットルールを再作成する必要があります。

<u> 再現手順 </u>:

1. **新規属性** を作成します（例：Test\_Attr）。
   * **ストア所有者のカタログ入力タイプ** = *テキスト* を設定します。
   * **Storefront プロパティ** で、「**プロモルール条件に使用** = *はい*」を設定します。
1. **新規属性セット** を作成します（例：Test\_Set）。
1. **新規属性** を **新規属性セット** に追加します（例：「Test\_Attr」属性を「Test\_Set」属性セットに追加）。
1. 3 つの製品を作成します。 例えば、次のように設定されます。
   * Product1, Test\_Attr = MAGT2NA\_Test3
   * Product2, Test\_Attr = 24-MB02
   * Product3, Test\_Attr = 701644329389M
1. ターゲット **ルール** （**マーケティング** を作成   > **関連製品ルール** を選択し、「**ルールを追加**」ボタンをクリックします。） 設定：
   * **適用先** = *関連製品*
   * **一致する製品**
   * 作成した新規属性 **in** **手順 1** を Product1 の属性に設定します（例：Test\_Attr = MAGT2NA\_Test3）。
   * **表示する製品** =他の 2 つの製品の属性（例：24-MB02 および 701644329389M 属性）。
1. **ルール** を保存します。
1. 必要に応じて、再インデックスを実行します。
1. キャッシュをクリアします。
1. フロントエンドで Product1 を開きます。

<u> 期待される結果 </u>:

関連製品が存在する。

<u> 実際の結果 </u>:

関連製品がありません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
