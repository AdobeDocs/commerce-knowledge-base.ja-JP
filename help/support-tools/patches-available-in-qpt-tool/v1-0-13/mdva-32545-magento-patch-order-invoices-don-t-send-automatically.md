---
title: 「MDVA-32545 パッチ：注文請求書が自動的に送信されない」
description: MDVA-32545 パッチを適用すると、管理者からの注文に対して請求書メールが顧客に自動的に送信されない問題が修正されます。 これは、**Braintree**または**PayPal Payflow Pro**など、**セール**取引タイプの支払い方法に影響します。
exl-id: 682eaeb1-5475-4d37-9536-0605f5b9f163
feature: Invoices, Orders
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# MDVA-32545 パッチ：注文請求書が自動的に送信されない

MDVA-32545 パッチを適用すると、管理者からの注文に対して請求書メールが顧客に自動的に送信されない問題が修正されます。 これは、以下を使用したあらゆる支払方法に影響します。 **販売** トランザクションタイプ（例：） **Braintree** または **PayPal Payflow Pro**.

このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.0.13 がインストールされています。 この問題は、Adobe Commerce バージョン 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.3.2-p2 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. を使用して任意の支払方法を有効にする **販売** トランザクションタイプ。 （例： **Braintree** または **PayPal Payflow Pro**.）
1. シンプルな製品を作成します。
1. フロントエンドに顧客アカウントを作成します。
1. 管理者から注文します。

<u>期待される結果</u>:

請求書のメールは、期待どおりに自動的にお客様に送信されます。

<u>実際の結果</u>:

請求書の E メールは、お客様に自動的には送信されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
