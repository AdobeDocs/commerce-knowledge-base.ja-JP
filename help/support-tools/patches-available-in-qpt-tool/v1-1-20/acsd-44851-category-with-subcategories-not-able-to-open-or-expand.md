---
title: 「ACSD-44851：サブカテゴリを含むカテゴリが開けない、または展開できない」
description: この記事では、ユーザーがサブカテゴリを持つカテゴリを開いたり展開したりできない問題の解決策について説明します。
exl-id: 46ad9f9d-ed66-44df-b66d-ab9ff3923c36
feature: Categories
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# ACSD-44851：サブカテゴリが開けない、または展開できないカテゴリ

ACSD-44851 パッチは、サブカテゴリを持つカテゴリをユーザーが開いたり展開したりできない問題を解決します。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.20 がインストールされています。 パッチ ID は ACSD-44851 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.0 ～ 2.4.5

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

サブカテゴリを含むカテゴリを開いたり展開したりできない。

<u>再現手順</u>:

1. Adobe Commerce Admin で、2 つのルートカテゴリとそれぞれのサブカテゴリを持つカテゴリツリーを作成します。
1. モバイルビュー/エミュレーターを開くか、レイアウトがモバイルになるまでウィンドウの幅を狭めます。
1. カタログのメインメニューを開きます。
1. ルートカテゴリを展開してみてください。
1. カテゴリを開いてみます。

<u>期待される結果</u>:

メニューにアクセスできます。

<u>実際の結果</u>:

モバイルメニューの 2 番目のレベルが開きません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [品質向上パッチ 「ツール」 > 「使用方法」](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) 『品質向上パッチツール』マニュアルの「」を参照してください。

* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) 『品質向上パッチツール』マニュアルの「」を参照してください。
