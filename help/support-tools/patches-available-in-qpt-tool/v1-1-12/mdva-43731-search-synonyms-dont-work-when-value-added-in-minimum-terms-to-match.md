---
title: 「MDVA-43731:「一致する最小用語」に値が追加されている場合、検索のシノニムが機能しない」
description: MDVA-43731 パッチでは、「一致する最小用語」に値が追加されると検索シノニムが機能しなくなる問題が修正されています。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.1.12 がインストールされている場合に利用できます。 パッチ ID は MDVA-43731。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。
exl-id: b795989c-d10b-443e-aebe-f3859930396a
feature: Cache, Marketing Tools, Search
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# MDVA-43731:[ 一致する最小用語 ] に値が追加されている場合、検索シノニムは機能しません

MDVA-43731 パッチでは、「一致する最小用語」に値が追加されると検索シノニムが機能しなくなる問題が修正されています。 このパッチは、 [品質向上パッチツール（QPT）](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) 1.1.12 がインストールされています。 パッチ ID は MDVA-43731。 この問題はAdobe Commerce 2.4.5 で修正される予定であることに注意してください。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.4.3 - 2.4.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがお使いのAdobe Commerceのバージョンと互換性があるかどうかを確認するには、 `magento/quality-patches` を最新バージョンにパッケージ化し、 [[!DNL Quality Patches Tool]：パッチの検索ページ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid). パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

「一致する最小用語」に値が追加されると、検索シノニムは機能しなくなります。

<u>再現手順</u>:

1. サンプルデータを使用してAdobe Commerceをインストールします。
1. Elasticsearch7 を検索エンジンとして設定します。
1. 「ジャケット」という単語を検索します。 製品のリストが表示されます。
1. パラメーターを追加 [4&lt;60%] 。対象： **設定** > **カタログ** > **カタログ検索** > **一致する最小用語**.
1. Config Cache をクリアし、再インデックスを実行します。
1. もう一度「ジャケット」という単語を検索し、製品のリストが表示されていることに注意してください。
1. に移動 **Marketing** > **SEO と検索** > **シノニムの検索**.
1. jacket、bagtecs、express plus という同義語を追加して、検索同義語を作成します。
1. 再インデックスを実行します。
1. 任意の同義語を使用して製品検索を実行します。 例：ジャケット。

<u>期待される結果</u>:

検索結果には、以前と同じ製品リストが表示されます。

<u>実際の結果</u>:

検索結果に製品が表示されません。

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス： [[ ソフトウェア アップデート ガイド ] > [ パッチを適用 ]](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html) 開発者向けドキュメントを参照してください。
* クラウドインフラストラクチャー上のAdobe Commerce: [「アップグレードとパッチ」 > 「パッチの適用」](https://devdocs.magento.com/cloud/project/project-patch.html) 開発者向けドキュメントを参照してください。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [品質向上パッチツールのリリース：品質向上パッチをセルフサービスで提供する新しいツール](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) サポートナレッジベースで。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかを確認します。](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md) サポートナレッジベースで。

QPT で使用可能なその他のパッチについては、を参照してください。 [QPT で使用可能なパッチ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) 開発者向けドキュメントを参照してください。
