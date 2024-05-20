---
title: 「MDVA-31282:Paypal PayFlow Pro の二重認証」
description: MDVA-31282 パッチは、Adobe Commerceの Paypal PayFlow Pro で二重認証が発生した場合の問題を解決します。 二重認証は、PayFlow Pro の不正フィルターをバイパスし、取引手数料を倍増させる効果もあります。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。
exl-id: f239012e-e1bd-474b-aad2-7218ec3a3d1b
feature: Orders, Payments
role: Admin
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# MDVA-31282: Paypal PayFlow Pro での二重認証

MDVA-31282 パッチは、Adobe Commerceの Paypal PayFlow Pro で二重認証が発生した場合の問題を解決します。 二重認証は、PayFlow Pro の不正フィルターをバイパスし、取引手数料を倍増させる効果もあります。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.7 がインストールされています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.3 および 2.3.5 ～ 2.3.6

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Adobe Commerceの PayPal PayFlow Pro では二重認証が行われ、PayFlow Pro の不正フィルターをバイパスして取引手数料を倍増させる効果があります。

<u>前提条件</u>:

PayPal PayFlow Pro 支払い方法を設定します。

<u>再現手順</u>:

1. ゲストカスタマーとしてフロントエンドに移動します。
1. への製品の追加 **ショッピングカート** 製品ページから。
1. 次の手順に進みます。 **チェックアウト**.
1. を指定 **発送先住所** 国\#1 の住所として（例：英国の住所）、配送方法を選択します。
1. を選択 **PayPal PayFlow Pro** 支払方法として。 を指定 **請求先住所** 国\#2 の住所として（例：米国の住所）。
1. クレジットカードのデータを入力し、注文します。
1. に移動します。 **売上** > **注文件数** を admin で実行し、作成された順序を確認します。

<u>期待される結果</u>:

* 「支払情報」ブロックが次のように表示されます。 *「トリガーされた不正フィルター：RESMSG：不正サービスによる審査中*. *注文は不正疑いステータスです」*.
* Paypal PayFlow Pro は、期待どおりに単一の承認トランザクションを表示します。

<u>実際の結果</u>:

* 「支払情報」ブロックが次のように表示されます。 *「トリガーされた不正フィルター：RESMSG：不正サービスによる審査中*. *注文は処理中ステータスです」*.
* Paypal PayFlow Pro は二重認証トランザクションを示しています。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
