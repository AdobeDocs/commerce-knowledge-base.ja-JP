---
title: 「MDVA-36718：カスタムオプションが API の変更後も残る」
description: MDVA-36718 Magentoパッチは、API を介して変更された後に古いカスタムオプションが残る問題を修正します。
exl-id: e9755764-e563-4921-af75-a90e06237053
feature: REST
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# MDVA-36718: API の変更後もカスタムオプションが残る

MDVA-36718 Magentoパッチは、API を介して変更された後に古いカスタムオプションが残る問題を修正します。

このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.0.22 がインストールされています。 パッチ ID は MDVA-36718。 この問題はMagentoバージョン 2.4.3 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

クラウドインフラストラクチャー 2.4.1 上のAdobe Commerce

**Magentoバージョンとの互換性：**

Adobe Commerce（すべてのデプロイメント方法） 2.3.0 ～ 2.4.2

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

<u>再現手順</u>:

1. シンプルな製品を作成します。
1. を追加 **ドロップダウンタイプ** カスタムオプション。
1. API を使用してカスタムオプションを更新する：送信 `PUT` リクエスト先 `/V1/products/options/{optionId}`.

<u>期待される結果</u>:

カスタムオプションは、期待どおりに更新されます。

<u>実際の結果</u>:

新しいカスタムオプションが追加されますが、古いカスタムオプションは残ります。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Magentoの問題に対するパッチをチェックします。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT ツールで使用可能なその他のパッチについては、を参照してください。 [QPT ツールで使用可能なパッチ](https://support.magento.com/hc/en-us/sections/360010506631-Patches-available-in-QPT-tool-) セクション。
