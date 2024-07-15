---
title: カタログのページネーションがElasticsearch 6.x で機能しない
description: この記事では、Elasticsearch 6.x でカタログのページネーションが機能しないAdobe Commerce問題に対するパッチを提供します。
exl-id: 60a423de-cf3a-4d73-a7cf-b6d9e95042ca
feature: Catalog Management, Categories, Search, Services
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# カタログのページネーションがElasticsearch 6.x で機能しない

この記事では、Elasticsearch 6.x でカタログのページネーションが機能しないAdobe Commerce問題に対するパッチを提供します。

以下のパッチは、Elasticsearch 6.x をカタログ検索エンジンとして使用するデプロイメントでAdobe Commerce 2.3.3 のユーザーが使用する問題を解決します。 検索結果の最初のページを超えて移動しようとすると、エラーメッセージが表示されます。

このパッチをインストールすると、ユーザーはすべての検索結果をページ表示できるようになります。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.3
* Adobe Commerce オンプレミス 2.3.3
* Magento Open Source 2.3.3
* Elasticsearch 6.x

## 問題

Magento Open Source、オンプレミスのAdobe Commerce、クラウドインフラストラクチャーのAdobe Commerceで、ページを切り替えても検索結果ページのページネーションが機能しない問題が発見されました。

<u> 再現手順 </u>:

1. Adobe Commerceをインストールします。
1. カタログ検索エンジンとして Elasticseach 6 を有効にします。
1. 管理者で設定された 1 ページの上限を超える製品をいくつかカテゴリに追加します。 **注意**:Adobe Commerce 2.3.3 で 1 ページに表示される商品のデフォルトの数は 12 です。
1. ストアフロントのカテゴリ（検索結果またはカテゴリページ）を開き、2 ページ目に移動します。

<u> 期待される結果 </u>:

製品は 2 番目のページに表示されます。

<u> 実際の結果 </u>:

**「***選択内容に一致する製品が見つかりません***」** のメッセージが 2 番目のページに表示されます。

## 解決策

この問題を修正するには、この記事に添付されているパッチを適用してください。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[ ダウンロード Elasticsearch 6.x パッチのカタログのページネーションの問題 ](assets/Catalog_pagination_issue_on_Elasticsearch_6_composer-2019-10-11-08-07-41.patch.zip) - パッチは、影響を受けるすべてのバージョンとエディションと互換性があります。

>[!WARNING]
>
>Adobeでは、症状が出ていない場合でも、できるだけ早くパッチを適用することを強くお勧めします。

## パッチの適用方法

手順については、[Adobe Commerceが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
