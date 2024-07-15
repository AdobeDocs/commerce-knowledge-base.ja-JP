---
title: 「MDVA-30594：複数のアドレスチェックアウトエラー」
description: MDVA-30594 パッチを使用すると、複数のアドレスで注文を行った後、お客様に注文成功ページが表示されない問題を解決できます。 Commerce管理者で注文を確認すると、正しい商品ではなく同じ商品を持つ 2 つの注文が表示されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。
exl-id: 7560cc39-ff0d-4313-979e-5cd588554c1d
feature: Checkout, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# MDVA-30594：複数のアドレス チェックアウト エラー

MDVA-30594 パッチを使用すると、複数のアドレスで注文を行った後、お客様に注文成功ページが表示されない問題を解決できます。 Commerce管理者で注文を確認すると、正しい商品ではなく同じ商品を持つ 2 つの注文が表示されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数の住所注文が注文成功ページで完了せず、正しい商品ではなく同じ商品を持つ 2 つの注文が表示されます。

<u> 前提条件 </u>:

ストアとストア表示を使用して 2 つの web サイトを作成します。

<u> 再現手順 </u>:

1. Web サイトカタログの **カタログ価格スコープ** を設定します（**店舗**/**設定**/**設定**/**カタログ**/**カタログ**/**価格**/**スコープ**）。
1. **固定製品税（FPT）** （**ストア**/**設定**/**販売**/**税**/**固定製品税**）を設定します。

   * **FPT を有効にする** = *はい*
   * **商品一覧に価格を表示** = *FPT を除く*
   * **製品表示ページに価格を表示** = *FPT を除く*
   * **販売モジュールの表示価格** = *FPT を除く* （**FPT** 摘要および最終価格を含む）
   * **メール表示価格**=*FPT を除く* （**FPT** 説明と最終価格を含む）
   * **FPT への税金適用** = *Yes*
   * **小計に FPT を含める** = *いいえ*

1. **FPT 属性** を作成して、デフォルトの属性セットに割り当てます。 （ユーザーガイドの [FPT の設定：FPT 属性の作成 ](https://docs.magento.com/user-guide/tax/fixed-product-tax-configuration.html#step-2-create-an-fpt-attribute) を参照してください）。

1. 4 つのシンプルな製品を作成し、**FPT** **属性値** を設定します（例：**FPT を設定**   **属性値** = *オーストラリア*）。

1. 次の設定で 2 つのバンドル製品を作成します。

   * 定義 **FPT**.
   * **Dynamic Price** = *No* を設定します。
   * Set **Price** = *100*.
   * バンドルオプションは一緒に出荷され、すべて **価格タイプ** = *固定* でデフォルトとしてマークされています。
   * 手順 4 で作成した簡単な製品を 2 つ追加します。

1. フロントエンドにユーザーアカウントを作成します。 住所をオーストラリアの住所（国をオーストラリアまたは **FPT** 設定で使用された国）に更新します。

1. 2 つのバンドルされた製品を買い物かごに追加します。

1. 買い物かごページに移動し、**FPT** が正しく表示されていることを確認します。

1. **複数のアドレスを使用してチェックアウト** をクリックします。

1. 2 番目のアドレスを追加します。

1. 各製品を異なるアドレスに割り当てます。

1. チェックアウトプロセスを **注文する** まで続行します。

1. **Place Order** ボタンをクリックします。

<u> 期待される結果 </u>:

複数のアドレスを持つ注文は正常に行われました。

<u> 実際の結果 </u>:

「*エラーが発生しました。*」が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
