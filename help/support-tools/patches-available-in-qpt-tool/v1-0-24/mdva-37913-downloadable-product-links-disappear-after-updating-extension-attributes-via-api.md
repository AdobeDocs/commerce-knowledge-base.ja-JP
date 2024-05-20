---
title: 「MDVA-37913:API を使用して拡張機能属性を更新すると、製品のダウンロードリンクが表示されなくなる」
description: の MDVA-37913 パッチでは、API を使用して拡張機能属性を更新した後、ダウンロード可能な製品リンクが消える問題を解決しています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.24 がインストールされている場合に利用できます。 パッチ ID は MDVA-37913。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。
exl-id: e4b2cf59-5c35-4a28-a63e-15cd7d0d5a5d
feature: REST, Attributes, Extensions, Products
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# MDVA-37913:API を使用して拡張機能属性を更新すると、製品のダウンロードリンクが表示されない

の MDVA-37913 パッチでは、API を使用して拡張機能属性を更新した後、ダウンロード可能な製品リンクが消える問題を解決しています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.24 がインストールされています。 パッチ ID は MDVA-37913。 この問題はAdobe Commerce 2.4.3 で修正される予定であることに注意してください。


## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**
クラウドインフラストラクチャー上のAdobe Commerce 2.3.6

**Adobe Commerce バージョンとの互換性：**
Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.0 - 2.4.0-p1
>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。


## 問題

API を使用して拡張機能属性を更新すると、ダウンロード可能な製品リンクが表示されなくなる。

<u>前提条件</u>：ダウンロードリンクを含むダウンロード可能な製品。

<u>再現手順</u>:

1. 次のようなリクエストを使用して、拡張機能の属性を更新します。

```JSON
{
    "product": {
        "extension_attributes": {
            "stock_item": {
                "is_in_stock": true,
                "qty": 100
            }
        }
    }
}
```

<u>期待される結果</u>:<br>
製品が更新されても、すべてのダウンロードリンクが削除されるわけではありません。

<u>実際の結果</u>:<br>
製品は更新されましたが、すべてのダウンロードリンクが削除されました。


## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe Commerce オンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html)

## 関連資料

サポートナレッジベースの品質向上パッチツールについて詳しくは、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) の節（サポートナレッジベース）を参照してください。
