---
title: 「ACSD-46703：製品のカスタマイズのドラッグ&ドロップが機能しない」
description: この記事では、製品のカスタマイズ可能なオプションのドラッグ&ドロップが期待どおりに動作しない問題の解決策を提供します。
exl-id: 49b29495-d225-4f34-ac76-b7294a86aea6
feature: Products
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# ACSD-46703：製品のカスタマイズのドラッグ&amp;ドロップが機能しない

ACSD-46703 パッチは、製品のカスタマイズ可能なオプション（ドラッグ アンド ドロップ）が期待どおりに動作しない問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.20 がインストールされている場合に使用できます。 パッチ ID は ACSD-46703 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.4 - 2.4.5

>[!NOTE]
>
>このパッチは、新しい [Quality Patches Tool] リリースを持つ他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

カスタマイズ可能なオプションをページ間でドラッグ&amp;ドロップすることはできません。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. シンプルな製品にカスタマイズ可能なオプションを追加し、20 を超えるオプションを追加してページネーションが発生することを確認します。
1. 同じページ内でカスタマイズ可能なオプションを移動（ドラッグ&amp;ドロップ）してみてください。
1. 次に、カスタマイズ可能なオプションをページ 2 からページ 1 に移動します。

<u> 期待される結果 </u>:

* カスタマイズ可能なオプションをページ間でドラッグ&amp;ドロップできます。
* 複数のページの場合でも、ドラッグ&amp;ドロップ機能を使用して値を並べ替えることができます。

<u> 実際の結果 </u>:

ドラッグ&amp;ドロップ機能を使用して値を別のページに移動することはできません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：品質パッチツールガイドの [ 品質パッチツール/使用状況 ](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/usage.html)。
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/check-patch-for-magento-issue-with-magento-quality-patches.html)。

QPT で使用可能なその他のパッチの詳細は、『品質向上パッチ ツール ガイド』の「[[!DNL Quality Patches Tool]：パッチの検索 ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)」を参照してください。
