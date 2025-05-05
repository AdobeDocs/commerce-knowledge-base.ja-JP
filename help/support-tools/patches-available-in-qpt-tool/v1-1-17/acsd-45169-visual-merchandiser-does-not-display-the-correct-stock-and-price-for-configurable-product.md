---
title: 「ACSD-45169：設定可能な製品の間違った在庫と価格がビジュアルマーチャンダイザーに表示される」
description: ACSD-45169 パッチは、ステージング更新が適用された後、ビジュアルマーチャンダイザーに設定可能な製品の正しい在庫と価格が表示されない問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.17 がインストールされている場合に利用できます。 パッチ ID は ACSD-45169 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。
exl-id: 5a7987c8-f276-4917-98f7-645402f4c454
feature: Categories, Configuration, Merchandising, Orders, Products
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# ACSD-45169：設定可能な製品の誤った在庫と価格がビジュアルマーチャンダイザーに表示される

ACSD-45169 パッチは、ステージング更新が適用された後、ビジュアルマーチャンダイザーに設定可能な製品の正しい在庫と価格が表示されない問題を修正しました。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.17 がインストールされている場合に使用できます。 パッチ ID は ACSD-45169 です。 この問題はAdobe Commerce 2.4.6 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.2-p2

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.1 ～ 2.4.4

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

ステージング更新が適用された後、ビジュアルマーチャンダイザーに、設定可能な製品の正しい在庫と価格が表示されません。

<u> 再現手順 </u>:

1. シンプルな製品を作成します。
1. シンプルな製品のスケジュールされた更新を作成します（必要なのは、異なる行 ID とエンティティ ID だけです）。
1. 設定可能な商品を作成します。
1. 設定可能な製品をカテゴリに割り当てます。
1. カテゴリを開き、「ビジュアルマーチャンダイザー」セクションで設定可能な製品を確認します。

<u> 期待される結果 </u>:

ビジュアルマーチャンダイザーに正しい在庫と価格が表示されます。

<u> 実際の結果 </u>:

ビジュアルマーチャンダイザーで間違った在庫と価格が表示される。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
