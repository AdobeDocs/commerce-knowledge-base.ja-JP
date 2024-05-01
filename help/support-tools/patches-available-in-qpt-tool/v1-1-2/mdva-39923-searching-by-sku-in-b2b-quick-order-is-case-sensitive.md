---
title: 「MDVA-39923:B2B での SKU による検索クイックオーダー機能では大文字と小文字が区別されます」
description: MDVA-39923 パッチでは、B2B クイックオーダー機能で SKU で注文を検索する際に、名前が保存されている場合とは異なるケースでエラーが発生する問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39923。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: 52e435df-28a7-49be-a257-7e5801601d57
feature: B2B, Catalog Management, Orders, Search
role: Admin
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# MDVA-39923:B2B での SKU による検索クイックオーダー機能では、大文字と小文字が区別されます

MDVA-39923 パッチでは、B2B クイックオーダー機能で SKU で注文を検索する際に、名前が保存されている場合とは異なるケースでエラーが発生する問題を修正しました。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.2 がインストールされています。 パッチ ID は MDVA-39923。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

B2B のクイックオーダー機能での SKU による検索では大文字と小文字が区別され、SKU が保存されたものとは異なる大文字と小文字が使用されている場合にエラーが表示されます。

<u>前提条件</u>:

B2B モジュールがインストールされている。

<u>再現手順</u>:

1. 管理者にログインし、に移動します。 **ストア** > **設定** > **B2B**.
1. Enable （有効） **共有カタログ** および **クイック注文**.
1. 大文字の SKU を使用して製品（TEST20-1234 など）を作成します
1. 作成した製品の割り当て **共有カタログ**.
1. 顧客としてログインし、 **クイック注文**.
1. SKU を小文字で入力します（例：test20-1234）。

<u>期待される結果</u>:

製品は、使用されているケースに関係なく見つかるはずです。

<u>実際の結果</u>:

次のエラーメッセージが表示されます。 *1 つの製品に注意が必要*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
