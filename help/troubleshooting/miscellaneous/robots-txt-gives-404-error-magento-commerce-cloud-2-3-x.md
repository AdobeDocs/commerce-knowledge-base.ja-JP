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

この記事では、次の場合の修正方法を説明します `robots.txt` クラウドインフラストラクチャー上のAdobe Commerceで、ファイルが 404 エラーをスローする。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

この `robots.txt` ファイルが機能せず、Nginx 例外をスローします。 この `robots.txt` ファイルは「その場」で動的に生成されます。 この `robots.txt` からファイルにアクセスできません `/robots.txt` Nginx にはすべて強制的にリダイレクトする書き換えルールがあるため、URL です `/robots.txt` に対するリクエスト `/media/robots.txt` 存在しないファイルです。

## 原因：

これは通常、Nginx が適切に設定されていない場合に発生します。

## 解決策

解決策は、リダイレクトする Nginx ルールを無効にすることです `/robots.txt` に対するリクエスト `/media/robots.txt` ファイル。 セルフサービスが有効なマーチャントは自分で実行でき、セルフサービスが有効でないマーチャントはサポートチケットを作成する必要があります。

セルフサービスが有効になっていない場合（または有効かどうかわからない場合）、 [Magentoサポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) から Nginx リダイレクト ルールの削除を要求しています `/robots.txt` に対するリクエスト `/media/robots.txt`.

セルフサービスを有効にしている場合は、ECE-Tools を 2002.0.12 以上にアップグレードし、の Nginx リダイレクトルールを削除してください `.magento.app.yaml` ファイル。 以下を参照してください。 [サイトマップと検索エンジンロボットを追加](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/robots-sitemap.html) 詳しくは、開発者ドキュメントを参照してください。

## 関連資料

* [Fastly レベルでMagento Commerce Cloudのために悪意のあるトラフィックをブロックする方法](/help/how-to/general/block-malicious-traffic-for-magento-commerce-on-fastly-level.md) サポートナレッジベースで。
* [サイトマップと検索エンジンロボットを追加](https://devdocs.magento.com/cloud/trouble/robots-sitemap.html) 開発者向けドキュメントを参照してください。
* [検索エンジンロボット](https://experienceleague.adobe.com/docs/commerce-admin/marketing/seo/seo-overview.html#search-engine-robots) を参照してください。
