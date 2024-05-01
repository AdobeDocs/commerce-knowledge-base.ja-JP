---
title: ページがキャッシュできないのでパフォーマンスが低下する
description: この記事では、キャッシュが必要なページ上のすべてのブロックで、ページキャッシュ（Fastly など）がいっぱいになったことが原因で web サイトの読み込み時間が増加したり停止したりした場合のソリューションを提供します。
exl-id: 7401d9bd-710c-4221-9c3d-d78042c1c1ad
feature: Cache, Categories
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# ページがキャッシュできないのでパフォーマンスが低下する

この記事では、キャッシュが必要なページ上のすべてのブロックで、ページキャッシュ（Fastly など）がいっぱいになったことが原因で web サイトの読み込み時間が増加したり停止したりした場合のソリューションを提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.x.x 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.x.x

### 問題

キャッシュ可能である必要があるが、に設定されているページにキャッシュブロックがあるので、サイトのパフォーマンスが低下します。 `cacheable="false"` .

### 原因：

Adobe Commerceでキャッシュする必要があるページがあります。 これらのページのスループットが最大です。 キャッシュからではなく、このような種類のページをリクエストするたびに、Adobe Commerceのパフォーマンスが低下します。

これらのページは次のとおりです。

* カタログ カテゴリ （PLP）
* 製品詳細ページ（PDP）
* 静的コンテンツページ（ホームページ、お問い合わせなど）

キャッシュ可能およびキャッシュ不可は、ページをキャッシュするかどうかを示すために使用される用語です。 デフォルトでは、すべてのページがキャッシュ可能です。 ただし、レイアウト内のいずれかのブロックがキャッシュ不可と指定されている場合、ページ全体をキャッシュできません。

以下のスクリーンショットは、設定を含むブロックを示しています `cacheable="false”`  キャッシュ**きないページを作成する**。

![non_cacheable_kb.png](assets/non_cacheable_kb.png)

キャッシュ不可ページの例としては、製品の比較、買い物かご、チェックアウトページがあります。

次のリストのページはキャッシュされません（Fastly、ブロック、レイアウトのキャッシュは回避されます）。 これは、レイアウトの「キャッシュ可能」な設定が原因で発生します。

### 解決策

上記のファイルに設定が含まれているかどうかを確認します。 `cacheable="false”` . 使用されている場合は、この設定が必要か必須かを確認します。

* 必要に応じて、キャッシュ不可ブロックをに移動することを検討します [プライベートコンテンツのメカニズム](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/cache/page-caching/private-content.html?itm_source=devdocs&amp;itm_medium=quick_search&amp;itm_campaign=federated_search&amp;itm_term=private%20co) その代わり。
* 不要な場合は、属性を削除します `cacheable="false”` を実行し、レイアウトキャッシュをフラッシュします。

>[!NOTE]
>
>クラウドインフラストラクチャー 2.4.1 以降でのAdobe Commerceの場合は、を使用できます。 [サイト全体分析ツール](https://docs.magento.com/user-guide/reports/site-wide-analysis-tool.html) を使用して、フルページキャッシュが正しく設定されているかどうかを自動的に確認できます。

### 関連資料

[Adobe Commerce キャッシュの概要](https://devdocs.magento.com/guides/v2.3/frontend-dev-guide/cache_for_frontdevs.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=cacheable%2) 開発者向けドキュメントを参照してください。
