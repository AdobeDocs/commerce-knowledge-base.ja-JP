---
title: 「MDVA-30837：送料無料の最小注文金額」
description: MDVA-30837 パッチは、送料計算の構成オプションを追加します。これにより、ユーザーは小計（または総計）に基づいて送料無料を受け取るための最小注文額を構成できます。 これにより、税金および配送方法をローカルでカスタマイズできます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。
exl-id: 64716d08-4ce0-40d5-aeb7-242e2aa85bb0
feature: Marketing Tools, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# MDVA-30837：送料無料の最小注文金額

MDVA-30837 パッチは、送料計算の構成オプションを追加します。これにより、ユーザーは小計（または総計）に基づいて送料無料を受け取るための最小注文額を構成できます。 これにより、税金および配送方法をローカルでカスタマイズできます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー 2.3.4-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.1 - 2.3.4-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

パッチ MDVA-30837 は、設定を追加して、小計（または総計）に基づいて送料無料を取得するように **最小注文額** 設定を設定します。

* **金額に税金を含める**:*Yes/No*。
   * **金額に税金を含む** が *Yes* に設定されている場合、最小受注金額は小計+税金 – 値引として計算されます。
   * **金額に税金を含む** が *No* に設定されている場合、最小注文金額は小計 – 割引として計算されます。

<u> 再現手順 </u>:

1. **ストア**/設定/**設定**/**営業**/**税** に移動して、以下を設定します。

   * *配送先住所* に基づく税金計算
   * クロスボーダー貿易を有効にする：*いいえ*
   * カタログに生産価格を表示：*税抜き*
   * 配送料の表示：*税抜き*
   * 表示価格：*税抜き*
   * 小計の表示 *税抜き*
   * 配送料の表示：*税抜き*
   * ギフト包装価格を表示：*税抜き*
   * 印刷されたカードの価格を表示する：*税別*
   * 受注合計に税金を含む：*Yes*
   * 全税金要約の表示：*Yes*

1. **営業**/**配送設定**/**送料無料** に移動し、**最小注文金額** = *30* を設定します。
1. **マーケティング**/プロモーション/**買い物かご価格ルール** に移動し、新しい価格ルールを作成します（手順について詳しくは、ユーザーガイドの [ 買い物かご価格ルールの作成 ](https://docs.magento.com/user-guide/marketing/price-rules-cart-create.html) を参照してください）。

   * クーポンコード = *特定のクーポン*。
   * 条件：小計が 25 ドル以上
   * アクション：送料無料= *一致する品目を含む出荷*。

1. 23.10 ドルの価格で製品を作成します。
1. デフォルトの税務処理基準に CA 税を追加します。
1. この商品を買い物かごに追加します。
1. 送料の見積もりを取得します。税引き後、総計=$25.01 で、送料無料が適用されます。
1. クーポンコードを適用します – 小計（税別）が 23.10 ドルであるため、有効になりません。

<u> 期待される結果 </u>:

追加の構成設定があります。「送料無料」構成内の「税金を金額に含める：*Yes*/*No*」

* 「税金を金額に含む」が *Yes* に設定されている場合、「最小受注金額」は「小計+税金 – 割引」として計算されます。
* 「金額に税金を含む」が「*No*」に設定されている場合、最小受注金額は「小計 – 値引」として計算されます。

<u> 実際の結果 </u>:

送料無料の価格ルール条件は小計に基づいてのみ設定でき、送料無料の方法は総計に基づいてのみ設定できます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
