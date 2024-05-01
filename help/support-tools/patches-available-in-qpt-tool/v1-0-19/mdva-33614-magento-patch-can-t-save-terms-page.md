---
title: 「MDVA-33614 パッチ：用語ページを保存できない」
description: 「MDVA-33614 パッチは、ページビルダーが次のエラーをスローするので、用語ページに編集を保存できない問題を修正しました。*ページビルダーの初期化中にエラーが発生しました。 テクニカルサポート担当者*にお問い合わせください。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.19 がインストールされている場合に利用できます。 パッチ ID は MDVA-33614。 この問題はAdobe Commerce 2.4.2 で修正されました。'
exl-id: d9b287bb-eab4-4c33-b725-ae0074962447
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# MDVA-33614 パッチ：用語ページを保存できません

MDVA-33614 パッチを適用すると、ページビルダーが次のエラーをスローするので、「用語」ページに編集内容を保存できない問題が修正されます。 *ページビルダーの起動中にエラーが発生しました。 テクニカル サポート担当者に問い合わせてください*. このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.19 がインストールされています。 パッチ ID は MDVA-33614。 この問題はAdobe Commerce 2.4.2 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Adobe Commerce バージョンとの互換性：** Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure 2.4.1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ページビルダーがエラーをスローするので、用語ページに編集を保存することは不可能です。

<u>再現手順</u>:

1. Commerce Admin で、に移動します。 **コンテンツ** > 要素 > **ページ**.
1. 「用語」ページを選択します。
1. クリック **編集**.
1. 編集して、 **保存**.

<u>期待される結果</u>:

ページはエラーなしで保存されます。

<u>実際の結果</u>:

次のエラーが表示されます。 *ページビルダーの起動中にエラーが発生しました。 テクニカル サポート担当者に問い合わせてください*.

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
