---
title: 「MDVA-29446：該当しない配送方法をチェックアウト可能」
description: MDVA-29446 パッチは、適用できない配送方法がチェックアウト配送方法オプションに表示され、選択すると、「*この方法の配送業者は null でフラット レートです*」というエラーメッセージが表示される問題を解決します。 が表示されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.6 がインストールされている場合に利用できます。 この問題は、今後のAdobe Commerce バージョンで修正される予定です。
exl-id: 74de5ec4-1f57-4d63-8fbc-614b23783ee3
feature: Checkout, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# MDVA-29446：関係のない配送方法をチェックアウトできます。

MDVA-29446 パッチは、適用できない配送方法がチェックアウト配送方法オプションに表示され、選択すると、「*この方法の配送業者は null でフラット レートです*」というエラーメッセージが表示される問題を解決します。 が表示されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.6 がインストールされている場合に使用できます。 この問題は、今後のAdobe Commerce バージョンで修正される予定です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.3-2.4.0。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

適用できない配送方法があるが、チェックアウトの配送方法オプションに表示される配送方法があり、この無関係な配送方法を選択できます。

<u> 再現手順 </u>:

1. clean 2.3-develop をインストールします。
1. 定額料金を有効にして次を設定します。

   * 「適用可能な国への出荷」 = *特定の国*
   * 特定の国に発送= *南極*
   * 該当しない場合はメソッドを表示= *はい*

1. その他の配送方法はすべて無効にしてください。
1. フロントエンドに移動し、米国の住所を持つ顧客を作成します。
1. 項目を選択し、「**買い物かごに追加**」をクリックします。
1. 買い物かごをクリックし、**チェックアウトに進む** をクリックします。

<u> 実際の結果 </u>:

1. **出荷** ページには、次の情報が表示されます。

   * 定率表示
   * 定率は$0
1. ユーザーが **次へ** をクリックすると、次のエラーが表示されます。

*「そのようなメソッドの通信事業者が見つかりません：null、flatrate」*

<u> 期待される結果 </u>:

* 配送方法が適用されない場合、配送方法の価格は表示されません。
* 「**次へ**」ボタンはアクティブにしないでください。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
