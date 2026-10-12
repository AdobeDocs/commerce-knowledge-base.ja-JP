---
title: Adobe Commerce on cloud infrastructureで起動するブロッカー
description: この記事では、Fastly設定、SSL証明書、301 リダイレクト、静的アセットのパフォーマンスに関する問題など、クラウドインフラストラクチャ上のAdobe Commerceで起動する際のブロッカーの修正について説明します。
exl-id: 3b2c331f-5d90-4051-ada1-4934538fce79
feature: Cache, Cloud, Marketing Tools, Observability, Paas
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: b673188e-f9fa-492a-b470-c8f949bf7827
    internal-label: Cache
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%
---
# Adobe Commerce on cloud infrastructureで起動するブロッカー

この記事では、Fastly設定、SSL証明書、301 リダイレクト、静的アセットのパフォーマンスに関する問題など、クラウドインフラストラクチャ上のAdobe Commerceで起動する際のブロッカーの修正について説明します。

## &#x200B;1. Fastly設定

[Fastly](https://www.fastly.com/)は、静的アセットを配信するためのVarnish ベースのコンテンツ配信ネットワーク （CDN）です。 本番環境のAdobe Commerce on cloud infrastructureでは必須であるため、ステージング環境と本番環境の両方で、Fastlyを有効にして設定したweb サイト（UAT）をFastlyで設定してテストすることが重要です。

>[!WARNING]
>
>フルページキャッシュ （FPC）が有効になっている場合、web サイトのパフォーマンスは異なります。本番稼働前に必ずテストしてください。

Fastlyの設定プロセスについて詳しくは、ユーザーガイドの「[Fastlyの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html)」トピックを参照してください。 ここでは、重要な手順を解説します。

### 1a. Fastly モジュールの最新バージョンがインストールされていることを確認します

最新の機能と改善点を入手するには、最新バージョンのFastly モジュールがインストールされていることを確認してください。 最新バージョンのFastlyがあるかどうかを確認するには、ユーザーガイドの[Fastly モジュールのアップグレード ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#upgrade-the-fastly-module)を確認してください。 詳しくは、ユーザーガイドの[Fastlyの設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html)を参照してください。

### 1b. Commerce管理者を使用したFastlyの有効化と設定

詳しくは、ユーザーガイドの「[Fastlyの資格情報を取得する](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#get-fastly-credentials)」を参照してください。

### 1c. Fastly VCL スニペットのアップロード

詳しくは、ユーザーガイドの「[VCLをFastlyにアップロード ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html)」を参照してください。

独自のVCL スニペットを[作成して追加することもできます](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html)。

### 1d. Fastly用のDNSの設定


詳細な手順については、この記事を参照してください。[ ユーザーガイドのFastly](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings)のセットアップ。

## &#x200B;2. 有効なSSL （TLS）証明書

問題：有効で動作するSSL証明書がなければ、ステージング環境のチェックアウトページで外部支払い方法をテストできません。

推奨事項&#x200B;**:** ステージングまたはライブドメイン名の共有SSL証明書をリクエストします。


## &#x200B;3. 301 リダイレクトの設定とテスト

問題：301 リダイレクトが提供されていないか、設定が不十分なため、ストアのSEO ランキングと検索リストが低下します。

推奨事項&#x200B;**:** 301 リダイレクトを慎重に設定してテストします。

古いweb サイトから新しいweb サイトに移行する場合、301 リダイレクトを使用すると、以前にインデックス化された古いページから新しいストアの適切なページに顧客を誘導できます。例えば、次のようになります。

http://www.mywebsite.com/old-category-page.html **>** http://www.mywebsite.com/new-seo-friendly-category-page.html

**関連する記事：**

* ユーザーガイドのroutes.yaml](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/routes/redirects.html)を通じて[ リダイレクトします。
* ユーザーガイドの[Cloud Console](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html)を通じてリダイレクトします。
* ユーザーガイドの[URL書き換え](https://experienceleague.adobe.com/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite.html)。

## &#x200B;4. アセットパフォーマンス

問題：静的なアセットの提供が遅いため、サイトのパフォーマンスが低下する（長い読み込み時間、マルチメディアコンテンツが表示されないなど）。 Web サイトの静的アセットは、CSS リソース、画像、ビデオ、添付ドキュメントなどです。 顧客がどのように整理され、提供されるかは、サイトのパフォーマンスを左右する重要な要素です。

推奨事項：パフォーマンスの低下の原因を特定するには、[Adobe Commerce Performance Toolkit](https://github.com/magento/magento2/tree/2.3/setup/performance-toolkit)をパフォーマンステストに使用することを検討してください。 また、次のようなサードパーティツールも検討できます。

* [包囲攻撃](https://www.joedog.org/siege): HTTP ロードテストとベンチマークユーティリティ。基本認証、Cookie、HTTP、HTTPS、およびFTP プロトコルをサポートします。
* [Jmeter](https://jmeter.apache.org/)：評判の良い負荷テストおよびパフォーマンス測定ツール。 急増トラフィック（例：フラッシュセールスなど）のパフォーマンスを測定するのに役立ちます。
* [New Relic](https://support.newrelic.com/): データ、クエリ、Redisなどの転送など、アクションごとに費やされたトラッキング時間でパフォーマンスの低下を引き起こすサイトのプロセスと領域を特定します。
* [WebPageTest](https://www.webpagetest.org/) （無料）および[Pingdom](https://www.pingdom.com/) （有料）: サイトページのリアルタイム分析は、異なるオリジンの場所で読み込まれます。

また、CSS、JavaScript、HTMLの[縮小](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html)を検討することもできます。

**関連する記事：**

* 開発者向けドキュメントの[ デプロイメントのテスト ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production.html)。
