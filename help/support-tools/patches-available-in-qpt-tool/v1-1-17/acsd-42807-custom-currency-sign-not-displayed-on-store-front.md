---
title: 「ACSD-42807：カスタムの通貨記号がストアフロントに表示されない」
description: ACSD-42807 パッチでは、カスタムの通貨記号がストアフロントに表示されない問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-42807 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 21bd17b4-d9d8-4c40-8f89-d6f7b930b475
feature: Storefront
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# ACSD-42807: ストアフロントにカスタムの通貨記号が表示されない

ACSD-42807 パッチでは、カスタムの通貨記号がストアフロントに表示されない問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.17 がインストールされています。 パッチ ID は ACSD-42807 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタムの通貨記号はストアフロントに表示されません。

<u>再現手順</u>:

1. に移動 **ストア** > **設定** > **設定** > **一般** > **通貨設定** 任意のカスタム通貨を選択します。 例： **ペソ （メキシコ）**.
1. に移動 **ストア** > **設定** > **設定** > **一般** > **ロケールオプション** を選択して、 **スペイン語（メキシコ）**.
1. に移動 **ストア** > **通貨記号** また、通貨記号をに設定します。 **MX$**.
1. フロントエンドの通貨記号を確認します。

<u>期待される結果</u>:

デフォルトの通貨記号は「MX$」で、通貨は「メキシコペソ」、ロケールは「スペイン語（メキシコ）」に設定されています。

<u>実際の結果</u>:

デフォルトの通貨記号は「$」です。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
