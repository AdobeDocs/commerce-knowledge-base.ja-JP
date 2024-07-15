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

ACSD-47669 パッチは、カスタマイズ可能なオプションを使用して製品の読み込み中に内部サーバーエラーが発生する問題を修正します。 このパッチは、[!DNL Quality Patches Tool (QPT)] 1.1.38 がインストールされている場合に使用できます。 パッチ ID は ACSD-47669 です。 この問題は、Adobe Commerce 2.4.6 で既に修正されています。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.5-p4

>[!NOTE]
>
>このパッチは、新しい [!DNL Quality Patches Tool] リリースを含む他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタマイズ可能なオプションを含む製品をインポートする際に、内部サーバーエラーが発生します。

<u> 再現手順 </u>:

1. 追加のストア表示を作成します。 ストアビューが 2 つあることを確認します（例：英国、英国）。
1. prod1 と prod2 など、2 つのシンプルなプロダクトを作成します。
1. 各ストア表示の製品と **すべてのストア表示** 範囲の製品の両方のカスタムオプションを追加する csv ファイルを準備します。 この csv ファイルを読み込みます。
1. 2 つのレコードを含む別の csv ファイルを準備します。 最初のレコードは「prod1」のカスタムオプションを特に英国のストア表示範囲について更新し、2 番目のレコードは「prod2」のカスタムオプションを **すべてのストア表示** 範囲について更新する必要があります。 この 2 つ目の CSV ファイルを読み込みます。

<u> 期待される結果 </u>:

エラーなくオプションをカスタマイズできるはずです。

<u> 実際の結果 </u>:

整合性制約違反エラーが発生しました。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：[[!DNL Quality Patches Tool] > Usage](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html) in the [!DNL Quality Patches Tool] guide.
* クラウドインフラストラクチャー上のAdobe Commerce：クラウドインフラストラクチャー上のCommerce ガイドの [ アップグレードとパッチ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html)/ パッチの適用」を参照してください。

## 関連資料

[!DNL Quality Patches Tool] について詳しくは、以下を参照してください。

* [[!DNL Quality Patches Tool]  リリース済み：品質パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) アドビのサポートナレッジベースに含まれています。
* [ を使用して、Adobe Commerceの問題にパッチが使用できるかどうかを  [!DNL Quality Patches Tool]](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで確認します。

QPT で使用可能なその他のパッチの詳細については、[!DNL Quality Patches Tool] ガイドの「[[!DNL Quality Patches Tool]: Search for patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
