---
title: ページがキャッシュできないのでパフォーマンスが低下する
description: この記事では、キャッシュが必要なページ上のすべてのブロックで、ページキャッシュ（Fastly など）がいっぱいになったことが原因で web サイトの読み込み時間が増加したり停止したりした場合のソリューションを提供します。
exl-id: 7401d9bd-710c-4221-9c3d-d78042c1c1ad
feature: Cache, Categories
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

キャッシュ可能である必要があるが `cacheable="false"` に設定されているキャッシュブロックがページに存在するため、サイトのパフォーマンスが低下します。

### 原因：

Adobe Commerceでキャッシュする必要があるページがあります。 これらのページのスループットが最大です。 キャッシュからではなく、このような種類のページをリクエストするたびに、Adobe Commerceのパフォーマンスが低下します。

これらのページは次のとおりです。

* カタログ カテゴリ （PLP）
* 製品詳細ページ（PDP）
* 静的コンテンツページ（ホームページ、お問い合わせなど）

キャッシュ可能およびキャッシュ不可は、ページをキャッシュするかどうかを示すために使用される用語です。 デフォルトでは、すべてのページがキャッシュ可能です。 ただし、レイアウト内のいずれかのブロックがキャッシュ不可と指定されている場合、ページ全体をキャッシュできません。

以下のスクリーンショットは、キャッシュ不可のページを作成する **&#x200B; **`cacheable="false"` 設定を持つブロックを示しています。

![non_cacheable_kb.png](assets/non_cacheable_kb.png)

キャッシュ不可ページの例としては、製品の比較、買い物かご、チェックアウトページがあります。

次のリストのページはキャッシュされません（Fastly、ブロック、レイアウトのキャッシュは回避されます）。 これは、レイアウトの「キャッシュ可能」な設定が原因で発生します。

### 解決策

上記の指定したファイルにという設定が `cacheable="false"` まれているかどうかを確認します。 使用されている場合は、この設定が必要か必須かを確認します。

* 必要に応じて、代わりに、キャッシュ不可ブロックを [ プライベートコンテンツメカニズム ](https://developer.adobe.com/commerce/php/development/cache/page/private-content/) に移動することを検討します。
* 不要な場合は、属性 `cacheable="false"` を削除し、レイアウトキャッシュをフラッシュします。

>[!NOTE]
>
>Cloud infrastructure 2.4.1 以降のAdobe Commerceでは、[Site-Wide Analysis Tool](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/site-wide-analysis-tool/access) を使用して、フルページキャッシュが正しく設定されていないかどうかを自動的に確認できます。

### 関連資料

開発者向けドキュメントの [Adobe Commerce キャッシュの概要 ](https://developer.adobe.com/commerce/frontend-core/guide/caching/)。
