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

MDVA-30594 パッチを使用すると、複数のアドレスで注文を行った後、お客様に注文成功ページが表示されない問題を解決できます。 Commerce管理者で注文を確認すると、正しい商品ではなく同じ商品を持つ 2 つの注文が表示されます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。 この問題は、Adobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

複数の住所注文が注文成功ページで完了せず、正しい商品ではなく同じ商品を持つ 2 つの注文が表示されます。

<u>前提条件</u>:

ストアとストア表示を使用して 2 つの web サイトを作成します。

<u>再現手順</u>:

1. を設定 **カタログの価格スコープ** （web サイトカタログ用）**ストア** > **設定** > **設定** > **カタログ** > **カタログ** > **価格** > **範囲**）に設定します。
1. 設定 **固定製品税（FPT）** （**ストア** > **設定** > **売上** > **税** > **固定製品税**）:

   * **FPT を有効にする** = *はい*
   * **製品リストに価格を表示** = *FPT を除く*
   * **製品ビューページに価格を表示** = *FPT を除く*
   * **販売モジュールに価格を表示** = *FPT を除く* 含む **FPT** 説明と最終価格）。
   * **価格をメールで表示** = *FPT を除く* 含む **FPT** 説明と最終価格）。
   * **FPT への税の適用** = *はい*
   * **小計に FPT を含める** = *不可*

1. を作成 **FPT 属性**&#x200B;を選択し、デフォルトの属性セットに割り当てます。 （詳しくは、 [FPT の設定：FPT 属性の作成](https://docs.magento.com/user-guide/tax/fixed-product-tax-configuration.html#step-2-create-an-fpt-attribute) （ユーザーガイドをご覧ください）。

1. 4 つのシンプルな製品を作成し、 **FPT** **属性値** （例： **FPT**   **属性値** = *オーストラリア*）に設定します。

1. 次の設定で 2 つのバンドル製品を作成します。

   * 定義 **FPT**.
   * を設定 **ダイナミック価格** = *不可*.
   * を設定 **価格** = *100*.
   * バンドルオプションは一緒に出荷され、すべてデフォルトとしてマークされました（） **価格タイプ** = *固定*.
   * 手順 4 で作成した簡単な製品を 2 つ追加します。

1. フロントエンドにユーザーアカウントを作成します。 住所をオーストラリアの住所（国をオーストラリアまたは使用されていた国に設定）に更新します **FPT** 設定）。

1. 2 つのバンドルされた製品を買い物かごに追加します。

1. カート ページに移動し、 **FPT** は正しく表示されています。

1. クリック **複数のアドレスを使用したチェックアウト**.

1. 2 番目のアドレスを追加します。

1. 各製品を異なるアドレスに割り当てます。

1. チェックアウト処理を次まで続行します **注文する**.

1. 「」をクリックします **注文する** ボタン。

<u>期待される結果</u>:

複数のアドレスを持つ注文は正常に行われました。

<u>実際の結果</u>:

のようなメッセージです。*エラーが発生しました。*」が表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
