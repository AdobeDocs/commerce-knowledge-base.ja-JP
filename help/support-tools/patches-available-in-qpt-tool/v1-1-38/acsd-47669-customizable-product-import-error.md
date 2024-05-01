---
title: 「ACSD-47669：カスタマイズ可能なオプションを含む製品をインポートする際の内部サーバーエラー」
description: ACSD-47669 パッチを適用すると、カスタマイズ可能なオプションを含む商品を読み込む際に内部サーバーエラーが発生するAdobe Commerceの問題を修正できます。
feature: Products
role: Admin, Developer
exl-id: 14afbd71-075a-4264-8da2-dbbd93f472a1
source-git-commit: 66e56b9ba31fd2c5d3f8a330f09d8e94df77b17d
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# ACSD-47669：カスタマイズ可能なオプションを含む製品をインポートする際の内部サーバーエラー

ACSD-47669 パッチは、カスタマイズ可能なオプションを使用して製品の読み込み中に内部サーバーエラーが発生する問題を修正します。 このパッチは、 [!DNL Quality Patches Tool (QPT)] 1.1.38 がインストールされています。 パッチ ID は ACSD-47669 です。 この問題は、Adobe Commerce 2.4.6 で既に修正されています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p4

>[!NOTE]
>
>パッチは、新しいを含む他のバージョンにも適用される可能性があります。 [!DNL Quality Patches Tool] リリース。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタマイズ可能なオプションを含む製品をインポートする際に、内部サーバーエラーが発生します。

<u>再現手順</u>:

1. 追加のストア表示を作成します。 ストアビューが 2 つあることを確認します（例：英国、英国）。
1. prod1 と prod2 など、2 つのシンプルなプロダクトを作成します。
1. 各ストア表示の製品と向けの両方のカスタムオプションを追加する csv ファイルを準備します **すべてのストア表示** スコープ。 この csv ファイルを読み込みます。
1. 2 つのレコードを含む別の csv ファイルを準備します。 最初のレコードは「prod1」のカスタムオプションを特に英国のストアビュースコープ向けに更新し、2 番目のレコードは「prod2」のカスタムオプションを英国向けに更新する必要があります **すべてのストア表示** スコープ。 この 2 つ目の CSV ファイルを読み込みます。

<u>期待される結果</u>:

エラーなくオプションをカスタマイズできるはずです。

<u>実際の結果</u>:

整合性制約違反エラーが発生しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[!DNL Quality Patches Tool] > 使用状況](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) が含まれる [!DNL Quality Patches Tool] ガイド。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html) （クラウドインフラストラクチャーのCommerce ガイド）を参照してください。

## 関連資料

について詳しくは、 [!DNL Quality Patches Tool]を参照してください。

* [[!DNL Quality Patches Tool] リリース済み：品質パッチをセルフサービスで適用する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [次を使用して、Adobe Commerceの問題にパッチが適用できるかどうかを確認します [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [[!DNL Quality Patches Tool]：パッチの検索](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) が含まれる [!DNL Quality Patches Tool] ガイド。
