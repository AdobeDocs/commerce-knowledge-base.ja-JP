---
title: 「MDVA-30815:Elasticsearchの空白の検索結果」
description: MDVA-30815 パッチは、検索結果のリミッタ オプションが変更されたときにElasticsearchが空白ページを表示する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ] （/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md） 1.0.7 がインストールされている場合に利用できます。 この問題はAdobe Commerce 2.3.5 で修正されました。
exl-id: dbe41a43-e248-407e-8cf9-319ad5843935
feature: Search, Services
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# MDVA-30815:Elasticsearchの空白の検索結果

MDVA-30815 パッチは、検索結果のリミッタ オプションが変更されたときにElasticsearchが空白ページを表示する問題を修正します。 このパッチは、[Quality Patches Tool （QPT） ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md)1.0.7 がインストールされている場合に使用できます。 この問題はAdobe Commerce 2.3.5 で修正されました。

## 影響を受ける製品とバージョン

**Adobe Commerce バージョン用のパッチが作成されます。**

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3

**Adobe Commerce バージョンとの互換性：**

* Adobe Commerce（すべてのデプロイメント方法） 2.3.2 ～ 2.3.3-p1

>[!NOTE]
>
>パッチは、新しい Quality Patches Tool リリースを使用する他のバージョンにも適用される可能性があります。 パッチがAdobe Commerceのバージョンと互換性があるかどうかを確認するには、`magento/quality-patches` パッケージを最新バージョンに更新し、[[!DNL Quality Patches Tool]: Search for patches page](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) で互換性を確認します。 パッチ ID を検索キーワードとして使用して、パッチを見つけます。

## 問題

Elasticsearchを使用している場合、検索結果のリミッターオプションを変更すると、Adobe Commerceに空白のページが表示されます。

<u> 前提条件 </u>:

Elasticsearchは **有効** です。 **STORES**/**Settings**/**Configuration**/**Catalog**/**Catalog Search** に移動します。

<u> 再現手順 </u>:

1. サイトに移動します。
1. メイン検索フィールドで製品を検索します。
1. 検索結果ページが表示されたら、検索結果ページの最後のページをクリックします。
1. リミッターオプションから「**ページごとに xx を表示**」を選択します。 これが現在設定されている検索結果数の上限と異なることを確認してください。

<u> 期待される結果 </u>:

このページには、設定された数の製品結果が表示されます。

<u> 実際の結果 </u>:

空白のページが表示されます。 このエラーは `var/report` にも見られます：*\&#39;&quot;0&quot;:&quot;SQLSTATE\[42000\]：構文エラーまたはアクセス違反：1064 SQL 構文にエラーがあります。near&#39;\&#39;を使用するための正しい構文については、MySQL サーバーのバージョンに対応するマニュアルを参照してください*

## パッチの適用

個々のパッチを適用するには、デプロイメント方法に応じて、次のリンクを使用します。

* Adobe CommerceまたはMagento Open Sourceオンプレミス：開発者向けドキュメントの [Software Update Guide > Apply Patches](https://devdocs.magento.com/guides/v2.4/comp-mgr/patching/mqp.html)
* クラウドインフラストラクチャー上のAdobe Commerce：開発者向けドキュメントの [ アップグレードとパッチ/パッチの適用 ](https://devdocs.magento.com/cloud/project/project-patch.html)。

## 関連資料

品質向上パッチツールの詳細については、次を参照してください。

* [ 品質向上パッチツールがリリースされました：品質向上パッチをセルフサービスで提供する新しいツール ](/help/announcements/adobe-commerce-announcements/magento-quality-patches-released-new-tool-to-self-serve-quality-patches.md) がサポートナレッジベースに追加されました。
* [Quality Patches Tool を使用して、Adobe Commerceの問題に対するパッチが使用可能かどうかをサポートナレッジベースで確認します ](/help/support-tools/patches-available-in-qpt-tool/check-patch-for-magento-issue-with-magento-quality-patches.md)。

QPT で利用可能なその他のパッチについて詳しくは、開発者向けドキュメントの [QPT で利用可能なパッチ ](https://devdocs.magento.com/quality-patches/tool.html#patch-grid) を参照してください。
