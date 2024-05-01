---
title: 「MDVA-33344 パッチ："rma-item"属性セット ID がハードコードされている」
description: MDVA-33344 パッチでは、データベースの値の代わりに、ハードコードされた「rma\_item」エンティティのデフォルト属性セット ID が使用される問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.16 がインストールされている場合に利用できます。 この問題は修正されました。また、Adobe Commerce 2.4.3 で修正される予定です。
exl-id: 2ef894a3-eea0-4f9f-8d26-984cd408458c
feature: Attributes, B2B
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# MDVA-33344 パッチ：「rma-item」属性セット ID がハードコードされている

MDVA-33344 パッチでは、データベースの値の代わりに、ハードコードされた「rma\_item」エンティティのデフォルト属性セット ID が使用される問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.16 がインストールされています。 この問題は修正されました。また、Adobe Commerce 2.4.3 で修正される予定です。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。** クラウドインフラストラクチャー上のAdobe Commerce 2.3.4

**Adobe Commerce バージョンとの互換性：** Adobe Commerce on cloud infrastructure およびAdobe Commerce オンプレミス 2.3.0 - 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

この `/rest/default/V1/returnsAttributeMetadata` 「rma\_item」エンティティのデフォルト属性セット ID がデフォルトのインストール ID と異なる場合、WebAPI エンドポイントは空の結果を返します。

<u>再現手順</u>:

に対して API 呼び出しを実行します。 `/rest/default/V1/returnsAttributeMetadata`.

<u>期待される結果</u>:

データが返されます。

<u>実際の結果</u>:

空の結果が返されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
