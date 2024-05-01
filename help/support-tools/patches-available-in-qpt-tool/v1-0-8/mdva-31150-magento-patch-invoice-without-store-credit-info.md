---
title: 「MDVA-31150：店舗クレジット情報のない請求書」
description: MDVA-31150 パッチは、店舗クレジット情報なしで請求書が作成される問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） v.1.0.8 がインストールされている場合に利用できます。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されることに注意してください。
exl-id: 70c87b67-6449-4285-9679-cca81613aa72
feature: Invoices, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# MDVA-31150：店舗クレジット情報のない請求書

MDVA-31150 パッチは、店舗クレジット情報なしで請求書が作成される問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) v.1.0.8 がインストールされている。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されることに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、cloud infrastructure 2.3.5-p2 上のAdobe Commerce用に設計されました。
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0 ～ 2.3.5-p2 および 2.4.0 ～ 2.4.0-p1 とも互換性があります。

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

API による請求書注文の後、使用済みの顧客残高とギフトカード情報は請求書に存在しません。

<u>再現手順</u>

1. 顧客アカウントへのストアクレジット金額の追加：管理サイドバーで、に移動します。 **顧客** > **すべてのお客様。**
1. 顧客レコードを見つけて、 **編集** 「アクション」列で、 **店舗クレジット** > 残高の更新 > **顧客の保存**.
1. ストアフロントに移動し、商品を買い物かごに追加します。
1. 店舗クレジットまたはギフトカード金額を一部支払として適用して注文を行います。
1. 次を使用して請求書を作成 `REST API>POST>/rest/V1/order/1/invoice` ペイロードを使用：    ```    { "capture": true, "items": [ { "extension_attributes": {}, "order_item_id": 3, "qty": 1 } ], "notify": true, "appendComment": true, "comment": { "extension_attributes": {}, "comment": "string", "is_visible_on_front": 0 }, "arguments": { "extension_attributes": {} }}    ```
1. を使用して作成された請求書を取得します `REST API>GET>/rest/V1/invoices/1`.

<u>期待される結果</u>

ストアクレジットとギフトカードの残高は、API 呼び出しによって返されます。

<u>実際の結果</u>

ストアのクレジットとギフトカードの残高は、API 呼び出しでは返されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
