---
title: 「MDVA-40619：階層の変更により CMS ページのインライン編集が中断され、500 エラーがスローされる」
description: MDVA-40619 パッチは、CMS ページ階層の変更によって CMS ページのインライン編集が中断され、「500 エラー」がスローされる問題を解決します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.5 がインストールされている場合に利用できます。 パッチ ID は MDVA-40619。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。
exl-id: c003d845-1ba0-49c0-9f1a-a4b0ec00f30c
feature: CMS
role: Admin
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# MDVA-40619：階層の変更により CMS ページのインライン編集が中断され、500 エラーがスローされる

MDVA-40619 パッチは、CMS ページ階層の変更によって CMS ページのインライン編集が中断され、「500 エラー」がスローされる問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.5 がインストールされています。 パッチ ID は MDVA-40619。 この問題はAdobe Commerce 2.4.4 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

CMS のページ階層が変更されると、CMS のページのインライン編集が中断し、「500 エラー」がスローされる。

<u>再現手順</u>:

1. 管理パネルに移動します。 **コンテンツ** > **階層**.
1. 「デフォルトのストア表示」を選択します。
1. 「親ノード階層を使用」のチェックを外します。
1. ページを手動で選択し、 **保存**.
1. その後、に移動します。 **コンテンツ** > **ページ**.
1. グリッドから CMS ページを編集してみてください。
1. クリック **保存**.

<u>期待される結果</u>:

ページが正常に保存されました。

<u>実際の結果</u>:

次のエラーが発生します。

*サーバーの技術的な問題によりエラーが発生しました。 やり直して、今までの作業を続けてください。 問題が解決しない場合は、後でもう一度試してください。*

`Error: Call to a member function getData() on null in /magento2ee/app/code/Magento/VersionsCms/Controller/Adminhtml/Cms/Page/InlineEdit/Plugin.php:62`

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-MQP-tool-) セクション。
