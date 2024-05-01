---
title: 「MDVA-39195：カテゴリページで「買い物かごに追加」が非アクティブになる」
description: MDVA-39195 パッチでは、買い物かごへのリダイレクトが有効な場合に、カテゴリページの**買い物かごに追加** ボタンが非アクティブになる問題が解決されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39195。 この問題はAdobe Commerce 2.4.3 で修正されました。
exl-id: de434908-e13a-4ab5-abb1-570bcc59c83d
feature: Categories, Orders, Shopping Cart
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# MDVA-39195：カテゴリ ページで [ 買い物かごに追加 ] が非アクティブになっている

MDVA-39195 のパッチを適用すると、 **カートに追加** 買い物かごへのリダイレクトが有効な場合、ボタンはカテゴリページで非アクティブになります。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.2 がインストールされています。 パッチ ID は MDVA-39195。 この問題はAdobe Commerce 2.4.3 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.2-p2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この **カートに追加** 買い物かごへのリダイレクトが有効な場合、ボタンはカテゴリページで非アクティブになります。

<u>再現手順</u>:

1. に移動 **ストア** > 設定 > **設定** > **売上** > **チェックアウト**.
1. を展開します。 **ショッピングカート** セクション。
1. を **買い物かごへの製品リダイレクトを追加した後** 「はい」に設定します。
1. カテゴリページにアクセスします。

<u>期待される結果</u>:

**カートに追加** はカテゴリページでアクティブです。

<u>実際の結果</u>:

**カートに追加** ボタンがカテゴリページで非アクティブです。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
