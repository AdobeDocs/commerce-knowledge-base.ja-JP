---
title: 「MDVA-31282:Paypal PayFlow Pro の二重認証」
description: MDVA-31282 パッチは、Adobe Commerceの Paypal PayFlow Pro で二重認証が発生した場合の問題を解決します。 二重認証は、PayFlow Pro の不正フィルターをバイパスし、取引手数料を倍増させる効果もあります。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。
exl-id: f239012e-e1bd-474b-aad2-7218ec3a3d1b
feature: Orders, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# MDVA-31282: Paypal PayFlow Pro での二重認証

MDVA-31282 パッチは、Adobe Commerceの Paypal PayFlow Pro で二重認証が発生した場合の問題を解決します。 二重認証は、PayFlow Pro の不正フィルターをバイパスし、取引手数料を倍増させる効果もあります。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.3 および 2.3.5 ～ 2.3.6

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Adobe Commerceの PayPal PayFlow Pro では二重認証が行われ、PayFlow Pro の不正フィルターをバイパスして取引手数料を倍増させる効果があります。

<u> 前提条件 </u>:

PayPal PayFlow Pro 支払い方法を設定します。

<u> 再現手順 </u>:

1. ゲストカスタマーとしてフロントエンドに移動します。
1. 製品ページから **買い物かご** に製品を追加します。
1. **チェックアウト** に進みます。
1. **配送先住所** を国\#1 の住所として指定し（例：英国住所）、配送方法を選択します。
1. 支払い方法として **PayPal PayFlow Pro** を選択します。 **請求先住所** を国\#2 の住所として指定します（例：USA 住所）。
1. クレジットカードのデータを入力し、注文します。
1. 管理で **営業**/**注文** に移動し、作成された注文を確認します。

<u> 期待される結果 </u>:

* 「Payment Information」ブロックに、「*&quot;Triggered Fraud Filters: RESMSG: Under review by Fraud Service* と表示されます。 *注文は不正の疑いがあるステータスです」*。
* Paypal PayFlow Pro は、期待どおりに単一の承認トランザクションを表示します。

<u> 実際の結果 </u>:

* 「Payment Information」ブロックに、「*&quot;Triggered Fraud Filters: RESMSG: Under review by Fraud Service* と表示されます。 *注文は処理中ステータスです」*。
* Paypal PayFlow Pro は二重認証トランザクションを示しています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
