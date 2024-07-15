---
title: robots.txt で、クラウドインフラストラクチャー上に 404 エラーのAdobe Commerceが表示される
description: この記事では、「robots.txt」ファイルがクラウドインフラストラクチャ上のAdobe Commerceで 404 エラーをスローする場合の修正方法を説明します。
exl-id: 6f0b9f47-1901-4c43-88d8-fd992015d70f
feature: Cloud, Marketing Tools, Paas
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# robots.txt で、クラウドインフラストラクチャー上に 404 エラーのAdobe Commerceが表示される

この記事では、クラウドインフラストラクチャ上のAdobe Commerceで `robots.txt` ファイルが 404 エラーをスローする場合の修正方法を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

`robots.txt` ファイルが機能せず、Nginx 例外がスローされる。 `robots.txt` ファイルは、「その場」で動的に生成されます。 Nginx には、存在しない `/robots.txt` ファイルにすべての `/robots.txt` リクエストを強制的にリダイレクトする書き換えルールがあるため、`/media/robots.txt` URL から `robots.txt` ファイルにアクセスできません。

## 原因：

これは通常、Nginx が適切に設定されていない場合に発生します。

## 解決策

解決策は、`/robots.txt` 要求を `/media/robots.txt` ファイルにリダイレクトする Nginx ルールを無効にすることです。 セルフサービスが有効なマーチャントは自分で実行でき、セルフサービスが有効でないマーチャントはサポートチケットを作成する必要があります。

セルフサービスが有効になっていない場合（または有効かどうかわからない場合）は、[Magentoサポートチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket)、Nginx リダイレクトルールの `/robots.txt` リクエストから `/media/robots.txt` リクエストへの削除をリクエストします。

セルフサービスを有効にしている場合は、ECE-Tools を 2002.0.12 以上にアップグレードし、`.magento.app.yaml` ファイルの Nginx リダイレクトルールを削除してください。 詳しくは、開発者向けドキュメントの [ サイトマップと検索エンジンロボットを追加する ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/robots-sitemap.html) を参照してください。

## 関連資料

* [ 悪意のあるトラフィックをブロックして、Fastly レベルでMagento Commerce Cloudする方法 ](/help/how-to/general/block-malicious-traffic-for-magento-commerce-on-fastly-level.md) については、サポートナレッジベースを参照してください。
* 開発者向けドキュメントの [ サイトマップと検索エンジンロボットを追加する ](https://devdocs.magento.com/cloud/trouble/robots-sitemap.html) を参照してください。
* ユーザーガイドの [ 検索エンジンロボット ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/seo/seo-overview.html#search-engine-robots)。
