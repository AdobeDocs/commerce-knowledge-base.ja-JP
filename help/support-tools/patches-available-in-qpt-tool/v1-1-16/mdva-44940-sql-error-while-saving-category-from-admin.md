---
title: 「MDVA-44940：管理者からカテゴリを保存中に SQL エラーが発生しました」
description: MDVA-44940 パッチを適用すると、管理者からカテゴリを保存中に SQL エラーが発生する問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.16 がインストールされている場合に利用できます。 パッチ ID は MDVA-44940。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: cae6f231-3b91-441f-af56-824db0fa2d32
feature: Admin Workspace, Categories, Sales Channels
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# MDVA-44940：管理者からカテゴリを保存中に SQL エラーが発生しました

MDVA-44940 パッチを適用すると、管理者からカテゴリを保存中に SQL エラーが発生する問題が修正されます。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.16 がインストールされている場合に使用できます。 パッチ ID は MDVA-44940。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3-p1

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

管理者からカテゴリを保存すると、SQL エラーが発生します。

<u> 再現手順 </u>:

1. サンプルデータをインストールします。
1. デフォルトカテゴリにストアグループを割り当てた 2 つ目の web サイトを作成します。

   * 新しいストアグループに割り当てるストア表示を作成します。

1. 在庫と、この在庫に割り当てられた追加のソース、および 2 つ目の web サイトに割り当てられた販売チャネルを作成します。
1. 2 つ目の web サイトに割り当てたテスト製品を作成します。
1. **管理者**/**カタログ**/**カテゴリ** に移動し、**範囲** = **2 番目の Web サイト** を選択して **カテゴリの製品**/**自動並べ替え**/在庫切れの製品を下部に移動して **保存** をクリックします。

<u> 期待される結果 </u>:

カテゴリが保存されます。

<u> 実際の結果 </u>:

次のエラーが発生します。*カテゴリの保存中に問題が発生しました*。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
