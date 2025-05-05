---
title: 「MDVA-43731:「一致する最小用語」に値が追加されている場合、検索のシノニムが機能しない」
description: MDVA-43731 パッチでは、「一致する最小用語」に値が追加されると検索シノニムが機能しなくなる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-43731。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: b795989c-d10b-443e-aebe-f3859930396a
feature: Cache, Marketing Tools, Search
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# MDVA-43731:[ 一致する最小用語 ] に値が追加されている場合、検索シノニムは機能しません

MDVA-43731 パッチでは、「一致する最小用語」に値が追加されると検索シノニムが機能しなくなる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.1.12 がインストールされている場合に使用できます。 パッチ ID は MDVA-43731。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「一致する最小用語」に値が追加されると、検索シノニムは機能しなくなります。

<u> 再現手順 </u>:

1. サンプルデータを使用してAdobe Commerceをインストールします。
1. Elasticsearch7 を検索エンジンとして設定します。
1. 「ジャケット」という単語を検索します。 製品のリストが表示されます。
1. パラメーター [4&lt;60%] を **Configuration** > **Catalog** > **Catalog Search** > **Minimum Terms to Match** に追加します。
1. Config Cache をクリアし、再インデックスを実行します。
1. もう一度「ジャケット」という単語を検索し、製品のリストが表示されていることに注意してください。
1. **マーケティング**/**SEO と検索**/**シノニムを検索** に移動します。
1. jacket、bagtecs、express plus という同義語を追加して、検索同義語を作成します。
1. 再インデックスを実行します。
1. 任意の同義語を使用して製品検索を実行します。 例：ジャケット。

<u> 期待される結果 </u>:

検索結果には、以前と同じ製品リストが表示されます。

<u> 実際の結果 </u>:

検索結果に製品が表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/quality-patches-tool/usage)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=ja) を参照してください。
