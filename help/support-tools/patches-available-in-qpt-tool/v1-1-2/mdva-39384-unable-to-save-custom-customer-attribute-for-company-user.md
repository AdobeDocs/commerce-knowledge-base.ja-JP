---
title: 「MDVA-39384：会社ユーザーのカスタム顧客属性を保存できない」
description: MDVA-39384 パッチを使用すると、会社ユーザーのカスタム顧客属性が保存されない問題を解決できます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.2 がインストールされている場合に利用できます。 パッチ ID は MDVA-39384。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: b9864ca6-307b-4649-b764-4512abc503d3
feature: Attributes, B2B, Companies
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# MDVA-39384：会社ユーザーのカスタム顧客属性を保存できません

MDVA-39384 パッチを使用すると、会社ユーザーのカスタム顧客属性が保存されない問題を解決できます。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.2 がインストールされています。 パッチ ID は MDVA-39384。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.1 ～ 2.3.6、2.4.1 ～ 2.4.3

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

会社ユーザーのカスタム顧客属性が保存されません。

<u>前提条件</u>:

B2B モジュールがインストールされている。

<u>再現手順</u>:

1. に移動 **ストア** > 設定 > **設定** > **B2B の機能** を設定して、 **会社を有効にする** 「はい」に設定します。
1. カスタム顧客属性を作成します。
   * 値必須：Yes （オプション。検証エラーが表示されるように有効化します）。
   * ストアフロントに表示：はい。
   * 使用するForms：すべての機能がリストに表示されます。
1. 会社を作成し、会社管理者としてログインします。
1. アカウントで会社構造に移動します。
1. 「」をクリック **ユーザーを追加** リンク。
1. カスタム属性を含むフォームに入力します。
1. クリック **保存**.

<u>期待される結果</u>:

カスタム属性値は、新しい会社ユーザーと共に保存されます。

<u>実際の結果</u>:

カスタム属性値は、新しい会社ユーザーと共に保存されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
