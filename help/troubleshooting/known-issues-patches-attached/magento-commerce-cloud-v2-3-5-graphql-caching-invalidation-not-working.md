---
title: クラウドインフラストラクチャー上のAdobe Commerce v2.3.5 GraphQL キャッシュの無効化が機能しない
description: この記事では、お客様が商品情報を変更した場合に、GraphQLの「GET」リクエストが古い情報を返す問題に対するパッチを提供します。
exl-id: 10ae52bd-e71a-42e3-9600-7a9713903815
feature: GraphQL, Cache, Categories, Cloud, Paas
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerce v2.3.5 GraphQL キャッシュの無効化が機能しない

この記事では、お客様が商品情報を変更した場合に、GraphQL `GET` リクエストが古い情報を返す問題に対するパッチを提供します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce v2.3.5.

## 問題

GraphQL リクエストは Fastly によってキャッシュされ、キャッシュされたバージョンは、Fastly からの後続のリクエストごとに取得されます。 商品がAdobe Commerce バックエンドで再保存されると、商品が更新されたときに Fastly キャッシュが無効になります。 ただし、引き続き有効です。

<u> 再現手順 </u>:

1. 次のGraphQL リクエストにトリガーを設定して、次のような特定のカテゴリの商品を取得します。
   <pre><magento2-server>
    </pre>
1. 上記のリクエストで取得した商品の 1 つをCommerce管理者に再保存します。
1. リクエストを再度トリガーします。

<u> 期待される結果 </u>:

`X-Cache` ヘッダーに `MISS` が含まれています。

<u> 実際の結果 </u>:

`X-Cache` ヘッダーには `HIT` が含まれます。これは、応答がキャッシュされることを意味します。

## 解決策

この記事で提供されているパッチを使用して、GraphQL製品キャッシュを無効にします。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-28559\_EE\_2.3.5-p1\_COMPOSER\_v1.patch](assets/MDVA-28559_EE_2.3.5-p1_v1.composer.patch.zip)

### 互換性のあるAdobe Commerceのバージョン：

パッチは次のために作成されました。

* クラウドインフラストラクチャー上のAdobe Commerce v2.3.5

このパッチは、次のAdobe Commerceのバージョンとエディションとも互換性があります（ただし、問題が解決しない可能性があります）。

* クラウドインフラストラクチャー上のAdobe Commerce v2.4.0
* Adobe Commerce オンプレミス v2.4.0
* クラウドインフラストラクチャー上のAdobe Commerce v2.3.5-p2
* Adobe Commerce オンプレミス v2.3.5-p2
* クラウドインフラストラクチャー上のAdobe Commerce v2.3.5-p1
* Adobe Commerce オンプレミス v2.3.5-p1
* Adobe Commerce オンプレミス v2.3.5
* クラウドインフラストラクチャー上のAdobe Commerce v2.3.4-p2
* Adobe Commerce オンプレミス v2.3.4-p2
* クラウドインフラストラクチャー上のAdobe Commerce v2.3.4
* Adobe Commerce オンプレミス v2.3.4
* Adobe Commerce オンプレミス v2.3.3-p1
* Adobe Commerce オンプレミス v2.3.3

## パッチの適用方法

Composer パッチの適用方法については、[Adobe提供の Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
