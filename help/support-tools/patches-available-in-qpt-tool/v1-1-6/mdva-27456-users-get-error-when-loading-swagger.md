---
title: 「MDVA-27456:Swagger の読み込み時にエラーが発生する」
description: MDVA-27456 パッチでは、Swagger を読み込もうとするとエラーが発生する問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp） 1.1.6 がインストールされている場合に利用できます。 パッチ ID は MDVA-27456。 この問題はAdobe Commerce 2.3.7 で修正されました。
exl-id: e331595f-a94b-4070-803a-60f559735b29
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# MDVA-27456:Swagger の読み込み時にエラーが発生する

MDVA-27456 パッチでは、Swagger を読み込もうとするとエラーが発生する問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html#mqp) 1.1.6 がインストールされています。 パッチ ID は MDVA-27456。 この問題はAdobe Commerce 2.3.7 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

Adobe Commerce（すべてのデプロイメント方法） 2.3.5-p1

**Adobe Commerce バージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.5 ～ 2.3.6-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Swagger の読み込み時にエラーが発生する。

<u>再現手順</u>:

に移動 `../swagger.`

<u>期待される結果</u>:

Swagger はエラーなしで読み込まれます。

<u>実際の結果</u>:

ユーザーに次のエラーが表示されます。 *API 定義を読み込めませんでした*. エラーログには次が含まれます。

*report.CRITICAL: レポート ID: webapi-5ea9c6da19cb1; メッセージ：「\DateTime」パラメータータイプが無効です。 パラメーターを確認し、もう一度試してください。*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、 [QPT で使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
