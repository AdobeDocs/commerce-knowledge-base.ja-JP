---
title: 「MDVA-40399：同じ注文の部分請求書を API を使用して同時に作成できない」
description: MDVA-40399 パッチは、Rest API を使用して同じ注文の部分的な請求書を同時に作成できない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.4 がインストールされている場合に利用できます。 パッチ ID は MDVA-40399。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 2444ba57-b30b-4fdf-9e5d-988cf7fa8dd1
feature: REST, Invoices, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# MDVA-40399：同じ注文の部分請求書を API で同時に作成することはできません

MDVA-40399 パッチは、Rest API を使用して同じ注文の部分的な請求書を同時に作成できない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.4 がインストールされています。 パッチ ID は MDVA-40399。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.2 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Rest API を使用して、同じ注文の部分請求書を同時に作成することはできません。

<u>前提条件</u>:

少なくとも 2 つのバリエーションを持つ設定可能な商品。

<u>再現手順</u>:

1. 設定可能な商品の両方のバリアントを買い物かごに追加します。
1. 注文します。
1. Rest API を使用して、注文に対して 2 つの請求書を同時に作成します。

<u>期待される結果</u>:

* 両方の請求書を正常に作成する必要があります。
* `qty_invoiced` で両方の請求書について更新する必要があります `sales_order_item` テーブル。
* 両方の製品に請求済数量が必要です。

<u>実際の結果</u>:

* 両方の請求書が正常に作成されました。
* `qty_invoiced` 次のいずれかの請求書に対して更新されません： `sales_order_item` テーブル。
* 管理画面 **Order View** ページでは、請求書数量は 1 つの製品に対してのみ表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
