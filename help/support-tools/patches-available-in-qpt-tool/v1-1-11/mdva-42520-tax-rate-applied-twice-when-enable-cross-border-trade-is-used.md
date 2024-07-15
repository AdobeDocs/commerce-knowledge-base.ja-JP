---
title: 「MDVA-42520:「クロスボーダー取引を有効にする」が使用された場合に 2 回適用される税率」
description: MDVA-42520 パッチは、**Enable Cross Border Trade**が使用されるときに税率が 2 回適用される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.11 がインストールされている場合に利用できます。 パッチ ID は MDVA-42520。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: c1ca44eb-fe92-4f28-807a-3a4563433386
feature: Catalog Management, Orders, Taxes
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# MDVA-42520:[ 国境を越えた貿易を有効にする ] が使用されている場合に 2 回適用される税率

MDVA-42520 パッチは、**Enable Cross Border Trade** が使用されるときに税率が 2 回適用される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.11 がインストールされている場合に使用できます。 パッチ ID は MDVA-42520。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

**クロスボーダー取引を有効にする** が使用されると、税率が 2 回適用されます。

<u> 再現手順 </u>:

1. **会社**、**共有カタログ** および **見積もり** を有効にする
1. スクリーンショットに従って税金を設定します。 **クロスボーダー取引** を必ず有効にしてください。

   ![ 税金設定 ](/help/support-tools/patches-available-in-qpt-tool/assets/tax_settings_1.png){width="700"}

1. ドイツ （10%）の税率を作成します。
1. 税率を適用する税務処理基準を作成します。
1. 会社とカスタム共有カタログを作成します。
1. 価格が 100 の製品を作成し、20% の価格割引でカスタム共有カタログに含めます。
1. ドイツ語の住所を持つ顧客を作成して、会社に割り当てます
1. 10 個の製品を顧客としてカードに追加します。
1. 買い物かごに移動して、見積もりを依頼します。
1. この見積もりをバックエンドで開いて、さらに 10% の割引を追加してみてください。

<u> 期待される結果 </u>:

見積の小計（税金を含む）および見積の総計（税金を含む） = $720

<u> 実際の結果 </u>:

見積の小計（税金を含む）および見積の総計（税金を含む） = $649.50。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
