---
title: 「MDVA-30972:REST API を使用して作成された注文ステータスの誤った出荷」
description: MDVA-30972 パッチは、REST API を使用した出荷作成時に注文ステータスが正しく変更されない問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。
exl-id: 70b8db1f-16d0-48f4-b0a2-483a7176cb89
feature: REST, Orders, Shipping/Delivery
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# MDVA-30972:REST API を使用して作成された注文ステータスの誤った出荷

MDVA-30972 パッチは、REST API を使用した出荷作成時に注文ステータスが正しく変更されない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 から 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

を使用して、注文の部分出荷が REST API を介して管理者から作成された場合 *詐欺の疑い* 注文ステータス、注文ステータスが「」に変更されます *処理*. それはにとどまるべきです *詐欺の疑い*.

<u>前提条件</u>:

* PayPal EC またはその他のオンライン支払い方法が設定されています。
* REST API の統合が設定されました。

<u>再現手順</u>:

1. 2 つ以上の項目で注文を作成します。
1. へのログイン **Admin** > **売上** > **注文件数**. 作成した注文を開きます。
1. 注文の詳細ページで、「」まで下にスクロールします **注文の合計**. 「」をクリック **ステータス** ドロップダウンして選択 *詐欺の疑い*. 次に、 **コメントを送信** ボタン。
1. 注文のステータスを確認 *詐欺の疑い* 現在の状態。
1. REST API を使用して、注文から 1 つの品目の出荷を作成します。

   ```
   * Method = `Post`
   * Header = `"{host}/rest/V1/orders/ {order_id}/ship"`
   * Body =
   ```

   ```
    {      "items": [        {          "extension_attributes": {},          "order_item_id": {order_item_id},          "qty": 1        }      ]    }
   ```

1. Admin で注文を再度開き、ステータスを確認します。

<u>期待される結果</u>:

* 注文ステータス = *詐欺の疑い*.
* 同じ出荷が管理者から作成された場合、注文ステータスは変更されません。

<u>実際の結果</u>:

注文ステータス = *処理*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
