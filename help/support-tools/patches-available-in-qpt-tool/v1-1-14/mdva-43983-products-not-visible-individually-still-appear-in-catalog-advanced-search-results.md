---
title: 「MDVA-43983:「個別に表示されない」と設定されている製品が検索結果に表示される」
description: MDVA-43983 パッチを適用すると、「個別に表示されない」に設定されている製品がカタログの詳細検索結果に表示されたままになる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.14 がインストールされている場合に利用できます。 パッチ ID は MDVA-43983。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: 2599fb6c-5b27-461b-9740-f586ae7df9f5
feature: Catalog Management, Products, Search
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# MDVA-43983:[ 個別に表示されない ] に設定された製品が検索結果に表示される

MDVA-43983 パッチを適用すると、「個別に表示されない」に設定されている製品がカタログの詳細検索結果に表示されたままになる問題が解決されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.14 がインストールされている場合に使用できます。 パッチ ID は MDVA-43983。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「個別に表示されない」に設定されている製品は、カタログの詳細検索結果に表示されます。

<u> 再現手順 </u>:

1. **ストア所有者のカタログ入力タイプ** として **ドロップダウン** または **ビジュアルスウォッチ** を持つ属性（カラーなど）を作成します。
1. **検索で使用** を **はい** に、**詳細検索で表示** を **はい** に設定します。
1. 属性オプションをいくつか追加します。
1. **表示** を持つ製品を **個別には表示されない** として作成します。
1. カラーアトリビュート オプションの割り当て。
1. ストアフロントの **カタログ詳細検索** ページに移動します。
1. カラー属性フィールドからカラー属性オプションのみを選択し、残りのフィールドは空白または空白のままにします。
1. 詳細検索フォームを送信します。
1. 検索結果を確認します。

<u> 期待される結果 </u>:

「個別に表示されない」と設定されている製品は、カタログの詳細検索結果に表示されません。

<u> 実際の結果 </u>:

「個別に表示されない」に設定されている製品は、カタログの詳細検索結果に表示されます。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) を参照してください。
