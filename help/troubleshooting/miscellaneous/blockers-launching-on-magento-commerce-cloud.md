---
title: クラウドインフラストラクチャー上のAdobe Commerceでブロックを開始
description: この記事では、Fastly 設定、SSL 証明書、301 リダイレクト、静的アセットのパフォーマンスに関連する問題など、クラウドインフラストラクチャ上でAdobe Commerceを起動するためのブロッカーの修正について説明します。
exl-id: 3b2c331f-5d90-4051-ada1-4934538fce79
feature: Cache, Cloud, Marketing Tools, Observability, Paas
role: Developer
source-git-commit: a3d11c96bac7922ea3c9d6eb4c19ebe1633da2d6
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceでブロックを開始

この記事では、Fastly 設定、SSL 証明書、301 リダイレクト、静的アセットのパフォーマンスに関連する問題など、クラウドインフラストラクチャ上でAdobe Commerceを起動するためのブロッカーの修正について説明します。

## &#x200B;1. Fastly の設定

[Fastly](https://www.fastly.com/) は、静的アセットを提供するためのワニス ベースのコンテンツ配信ネットワーク（CDN）です。 これは実稼動環境のクラウドインフラストラクチャー上のAdobe Commerceに必要なので、Fastly を設定し、Fastly を有効化および設定した web サイト（UAT）を、ステージング環境と実稼動環境の両方でテストすることが重要です。

>[!WARNING]
>
>フルページキャッシュ（FPC）を有効にすると、web サイトのパフォーマンスが異なります。運用開始前にテストしてください。

Fastly の設定プロセスについては、ユーザーガイドの [Fastly の設定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) トピックで詳しく説明しています。 重要な手順は次のとおりです。

### 1a. 最新バージョンの Fastly モジュールがインストールされていることを確認してください

最新バージョンの Fastly モジュールをインストールして、最新の機能と改善点を取得してください。 最新バージョンの Fastly をお持ちかどうかを確認するには、アドビのユーザーガイドで [Fastly モジュールをアップグレード &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#upgrade-the-fastly-module) を確認してください。 詳しくは、ユーザーガイドの [Fastly の設定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) を参照してください。

### 1b. Commerce Admin を使用した Fastly の有効化と設定

詳しくは、ユーザーガイドの [Fastly の資格情報を取得する &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#get-fastly-credentials) を参照してください。

### 1c. Fastly VCL スニペットのアップロード

詳しくは、ユーザーガイドの [Fastly への VCL のアップロード &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) を参照してください。

[&#x200B; 独自のカスタム VCL スニペットを作成して追加する &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html) こともできます。

### 1d. Fastly の DNS の設定


詳細な手順については、ユーザーガイドの [Fastly の設定 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings) を参照してください。

### サポートナレッジベースの関連する Fastly 記事

* [Fastly キャッシュがクラウドで機能しない](/help/troubleshooting/miscellaneous/fastly-caching-is-not-working-on-magento-cloud.md)

## 2.有効な SSL （TLS）証明書

問題：有効で機能する SSL 証明書がないと、ステージング環境のチェックアウトページで外部支払い方法をテストできません。

推奨事項 **:** ステージングまたはライブドメイン名の共有 SSL 証明書をリクエストします。


## &#x200B;3. 301 リダイレクトの設定とテスト

問題：301 リダイレクトが提供されないか、設定が不十分で、SEO ランキングと検索リストでストアがドロップする原因になります。

推奨事項 **:** 301 リダイレクトの設定とテストを慎重に行ってください。

古い web サイトから新しい web サイトに移行する場合は、以前にインデックスを作成した古いページから新しいストアの適切なページに顧客が 301 リダイレクトされます。例えば、次のようになります。

http://www.mywebsite.com/old-category-page.html **>** http://www.mywebsite.com/new-seo-friendly-category-page.html

**関連記事：**

* [routes.yaml を使用したリダイレクト &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/routes/redirects.html) をユーザガイドで説明しています。
* ユーザーガイドの [Cloud Console を使用したリダイレクト &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html)。
* ユーザーガイドの [URL の書き換え &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite.html)。

## 4.アセットのパフォーマンス

問題：静的アセットの提供に時間がかかるので、サイトのパフォーマンスが低下します（読み込み時間が長くなる、マルチメディアコンテンツが表示されない、など）。 Web サイトの静的アセットには、CSS リソース、画像、ビデオ、添付ドキュメントなどがあります。 サイトのパフォーマンスの重要な要因は、コンテンツを整理し、提供する方法です。

推奨事項：パフォーマンスが低下した原因を特定するには、パフォーマンステストに [Adobe Commerce Performance Toolkit](https://github.com/magento/magento2/tree/2.3/setup/performance-toolkit) を使用することを検討してください。 次のサードパーティツールも検討できます。

* [Siege](https://www.joedog.org/siege-home): HTTP 負荷テストおよびベンチマークユーティリティ。基本認証、Cookie、HTTP、HTTPS および FTP プロトコルをサポートします。
* [Jmeter](https://jmeter.apache.org/)：評判の良い負荷テストおよびパフォーマンス測定ツール。 スパイクされたトラフィックのパフォーマンスを測定するのに役立ちます（例：フラッシュセールス）。
* [New Relic](https://support.newrelic.com/): サイトのプロセスと領域を特定し、データ、クエリ、Redis などの送信に費やした時間がアクションごとに追跡されるため、パフォーマンスが低下する原因になります。
* [WebPageTest](https://www.webpagetest.org/) （無料）および [Pingdom](https://www.pingdom.com/) （有料）：サイトページのリアルタイム分析により、異なるオリジンの場所に時間を読み込みます。

CSS、JavaScriptおよびHTMLの [&#x200B; 縮小 &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html) も検討できます。

**関連記事：**

* 開発者向けドキュメントの [&#x200B; デプロイメントをテスト &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production.html) します。
