---
title: 「MDVA-37224:PayFlow Pro で「交渉可能な見積もり」を支払えない」
description: Paypal PayFlow Pro で**譲渡可能見積もり**の支払いができない場合は、MDVA-37224 パッチで問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.0.23 がインストールされている場合に利用できます。 パッチ ID は MDVA-37224。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。
exl-id: df75b38d-64c8-46b5-85ff-7606ce1dfd34
feature: B2B, Orders, Payments, Quotes
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# MDVA-37224: PayFlow Pro で「譲渡性見積」を支払えない

お客様が料金を支払えない場合、MDVA-37224 パッチで問題が修正されます **譲渡可能見積** Paypal PayFlow Pro を使用する。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.23 がインストールされています。 パッチ ID は MDVA-37224。 この問題はAdobe Commerce バージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

* このパッチは、クラウドインフラストラクチャー 2.3.6-p1 上のAdobe Commerce用に設計されました
* また、このパッチは、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.3-2.4.2-p1 とも互換性があります

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>前提条件</u>:

* B2B モジュールがインストールされたAdobe Commerce
* 会社機能が有効
* **譲渡可能見積** 有効な機能
* 会社ユーザーが存在します
* PayPal PayFlow Pro 支払い方法が有効になり、設定されました
* PayPal PayFlow Pro 支払い方法は B2B で許可されています
* 異なる価格の 2 つの製品が作成されました

<u>再現手順</u>:

1. ストアフロントを開きます。
1. 追加 **製品 1** 買い物かごに移動します。
1. を作成 **譲渡可能見積** （用） **製品 1**.
1. 追加 **製品 2** 買い物かごに移動します。
1. 管理者から、を受け入れます **譲渡可能見積** 作成手順 3.
1. ストアフロントからこれを開きます **譲渡可能見積** チェックアウトに進みます。
1. 「」を選択します **支払い方法** = *PayPal PayFlow Pro* 時刻 **レビューと支払い** ステップ。
1. 注文します。

<u>期待される結果</u>:

* 注文は正常に行われました。
* PayPal は、期待どおりに正しい情報を含むメールを顧客に送信します。

<u>実際の結果</u>:

* Web ページがハングし、注文が完了しない。
* PayPal は、次の例のように、値が 0 の確認を顧客に送信します。

```php
Order ID: A1xxxxxxxxx
Order Placed: Monday, April 21, 2021 01:12:12 PM PDT

Shipping Amount: $0.00
Tax Amount: $0.00
Amount of Transaction: $0.00
Payment Type: Visa

BILL TO
--------
US
```


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* 
   * [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
