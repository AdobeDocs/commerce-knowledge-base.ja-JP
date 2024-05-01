---
title: 「MDVA-39153：管理者での並べ替え中に、割引額が正しく計算されない」
description: MDVA-39153 パッチは、管理者での並べ替え時に割引額が正しく計算されない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.8 がインストールされている場合に利用できます。 パッチ ID は MDVA-39153。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: d4d11bea-a528-4eb5-8a57-8a7330975e4a
feature: Admin Workspace, Orders, Personalization, Payments
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# MDVA-39153：管理画面での並べ替え中に、割引額が正しく計算されない

MDVA-39153 パッチは、管理者での並べ替え時に割引額が正しく計算されない問題を修正します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.8 がインストールされています。 パッチ ID は MDVA-39153。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p1 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者で並べ替え中に、割引額が正しく計算されません。

<u>再現手順</u>:

1. に移動します **Admin** > **ストア** > **設定** > **売上** > **税金**.
1. ショッピングカートに税金を表示して、配送用の税金をオンにします。
1. テーブルの料金配送方法（$15）を有効にして設定します。
1. 組み込み税率（CA）の税務処理基準を作成します。
1. 買い物かご全体と配送額に固定の$5 割引を適用する買い物かご価格ルールを作成します。
1. 価格が 12 ドルの商品を買い物かごに追加し、買い物かごページに移動します。
1. 割引を買い物かごに適用します。
1. 「見積り」セクションの配送方法を「定額料金」に設定します。
1. レビュー手順までチェックアウトを進めます（注文を行わないでください）。
1. ホームページに移動し、買い物かごに戻ります。
1. 「見積もり」セクションの発送方法を「テーブルレート」に変更しました。

<u>期待される結果</u>:

割引率は変わりません – 5 ドル。

<u>実際の結果</u>:

値引きは 6 ドル 31 です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
