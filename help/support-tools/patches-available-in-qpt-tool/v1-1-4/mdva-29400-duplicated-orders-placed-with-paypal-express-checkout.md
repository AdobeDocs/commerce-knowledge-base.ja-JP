---
title: 「MDVA-29400:PayPal Express Checkout で注文が重複する」
description: MDVA-29400 パッチは、お客様が PayPal Express Checkout で注文を行う際に重複した注文が作成される問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.4 がインストールされている場合に利用できます。 パッチ ID は MDVA-29400。 この問題はAdobe Commerce 2.4.1 で修正されました。
exl-id: 75b943c8-5f7c-4d94-ae92-935428fdfcf8
feature: Checkout, Orders, Payments
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# MDVA-29400:PayPal Express チェックアウトで注文が重複する

MDVA-29400 パッチは、お客様が PayPal Express Checkout で注文を行う際に重複した注文が作成される問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.4 がインストールされています。 パッチ ID は MDVA-29400。 この問題はAdobe Commerce 2.4.1 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.3.7-p1、2.4.0 ～ 2.4.0-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

重複した注文は、ユーザーが PayPal Express Checkout で注文を行うと作成されます。

<u>前提条件</u>:

PayPal Express チェックアウトを有効にして設定。

<u>再現手順</u>:

1. 商品を買い物かごに追加します。
1. チェックアウトページに移動し、支払い方法として PayPal Express を使用します。
1. Paypal/express/review/ ページにリダイレクトされます。
1. 注文する。 成功ページにリダイレクトされます。
1. PayPal/express/review/Page に戻ります。
1. 「」をクリック **注文する** ボタン。

<u>期待される結果</u>:

1 つの注文のみが作成されます。

<u>実際の結果</u>:

次のエラーが発生します。 *PayPal Express チェックアウトトークンが存在しません*&#x200B;しかし、2 番目の注文が正常に行われます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
