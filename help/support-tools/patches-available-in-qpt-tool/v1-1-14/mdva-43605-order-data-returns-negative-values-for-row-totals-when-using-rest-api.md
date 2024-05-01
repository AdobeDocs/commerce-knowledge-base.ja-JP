---
title: 「MDVA-43605:Rest API を使用している場合、注文データが行の合計に対して負の値を返す」
description: MDVA-43605 パッチでは、Rest API を使用する際に、注文データが行の合計に対して負の値を返す問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-43605。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 8a679e85-1681-42c3-b072-18797198bdc4
feature: REST, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# MDVA-43605:Rest API を使用している場合、注文データが行の合計に対して負の値を返す

MDVA-43605 パッチでは、Rest API を使用する際に、注文データが行の合計に対して負の値を返す問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.14 がインストールされています。 パッチ ID は MDVA-43605。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.1 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Rest API を使用する場合、注文データは行の合計に対して負の値を返します。

<u>再現手順</u>:

1. 送料無料を有効にします。
1. に移動します。 **設定** > **カタログ** > **価格** > and set Catalog Price Scope = Website.（カタログの価格範囲= ウェブサイト）を選択します。
1. に移動します。 **設定** > **売上** > **税** を更新します。
   * 出荷の税金区分=課税品
   * 計算設定：
      * カタログ価格=税込
      * 送料=込み価格
      * 価格に対する割引の適用=税込
   * 価格表示設定：税を含む（すべてのフィールド）
   * 買い物かごの表示設定：税を含む（すべてのフィールド）
   * 受注、請求書、クレジット・メモ：
      * 出荷金額の表示=税込
1. 米国の税率（都道府県= &#39;*&#39;）、税率= 24.00 を作成します。
1. 前述の税率で税務処理基準を作成します。
1. 特定のクーポンを使用して買い物かご価格ルールを作成します。割引額= $50 の固定金額を買い物かご全体に適用します。
1. 次の価格で 4 つの製品を作成します。8.90 ドル、5.90 ドル、6.90 ドル、および 5.95 ドル。
1. 前の手順で作成したクーポンコードを使用して、これらの 4 つの製品を含む管理注文を作成します。 送料無料をご利用ください。
1. クーポンコードは買い物かごの合計をカバーしているので、支払いは必要ありません。
1. Rest API エンドポイントを使用して作成された注文を取得します。

   ```json
   GET rest/V1/orders/1
   ```

<u>期待される結果</u>:

の値 `base_row_total` および `base_row_total_incl_tax` 応答のがゼロです。

<u>実際の結果</u>:

この `base_row_total` および `base_row_total_incl_tax` 応答のフィールドに負の値があります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
