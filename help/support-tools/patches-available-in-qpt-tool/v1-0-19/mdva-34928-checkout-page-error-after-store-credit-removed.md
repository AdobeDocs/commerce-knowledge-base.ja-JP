---
title: 「MDVA-34928：ストアクレジットが削除された後のチェックアウトページエラー」
description: MDVA-34928 パッチは、ストアクレジットを削除した後、チェックアウトページに無限ローダーが存在する問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-34928。 この問題はAdobe Commerce 2.3.6 で修正されました。
exl-id: 9ef6777a-88c8-4fed-a296-0cb4e6ad153a
feature: Checkout, Orders, Returns, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# MDVA-34928：店舗クレジット削除後のチェックアウト ページ エラー

MDVA-34928 パッチは、ストアクレジットを削除した後、チェックアウトページに無限ローダーが存在する問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-34928。 この問題はAdobe Commerce 2.3.6 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー上のAdobe Commerce 2.3.5-p2

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.3.5 - 2.3.5-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ストアクレジットを削除した後、チェックアウトページに無限ローダーがあります。

<u>再現手順</u>:

1. 顧客アカウントを作成します。
1. 買い物かごに追加できる商品を決定します – 価格をメモします。
1. 管理者でアカウントを編集します。
1. クリック **店舗クレジット**.
1. 商品の価格に対応する金額を追加します。
1. ストアフロントで顧客としてログインします。
1. 商品を買い物かごに追加します。
1. チェックアウトに進みます。
1. 店舗クレジットを適用します。
1. ストアクレジットを削除してみてください。

<u>期待される結果</u>:

店舗クレジットが削除されます。

<u>実際の結果</u>:

ページが更新されるまで、無限ローダーがスピンします。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
