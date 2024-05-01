---
title: クラウドインフラストラクチャー上のAdobe Commerceでブロックを開始
description: この記事では、Fastly 設定、SSL 証明書、301 リダイレクト、静的アセットのパフォーマンスに関連する問題など、クラウドインフラストラクチャ上でAdobe Commerceを起動するためのブロッカーの修正について説明します。
exl-id: 3b2c331f-5d90-4051-ada1-4934538fce79
feature: Cache, Cloud, Marketing Tools, Observability, Paas
role: Developer
source-git-commit: 3dd44b72bc9f02fe808b70355c4331fc28aa3606
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# クラウドインフラストラクチャー上のAdobe Commerceでブロックを開始

この記事では、Fastly 設定、SSL 証明書、301 リダイレクト、静的アセットのパフォーマンスに関連する問題など、クラウドインフラストラクチャ上でAdobe Commerceを起動するためのブロッカーの修正について説明します。

## 1. Fastly の設定

[Fastly](https://www.fastly.com/) は、静的アセットを提供するためのワニス ベースのコンテンツ配信ネットワーク（CDN）です。 これは実稼動環境のクラウドインフラストラクチャー上のAdobe Commerceに必要なので、Fastly を設定し、Fastly を有効化および設定した web サイト（UAT）を、ステージング環境と実稼動環境の両方でテストすることが重要です。

>[!WARNING]
>
>フルページキャッシュ（FPC）を有効にすると、web サイトのパフォーマンスが異なります。運用開始前にテストしてください。

Fastly 設定のプロセスについては、以下で詳しく説明します。 [Fastly の設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) トピックを参照してください。 重要な手順は次のとおりです。

### 1a. 最新バージョンの Fastly モジュールがインストールされていることを確認してください

最新バージョンの Fastly モジュールをインストールして、最新の機能と改善点を取得してください。 最新バージョンの Fastly があるかどうかを確認するには、以下を確認します。 [Fastly モジュールのアップグレード](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#upgrade-the-fastly-module) を参照してください。 詳しくは、を参照してください。 [Fastly の設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) を参照してください。

### 1b. Commerce Admin を使用した Fastly の有効化と設定

詳しくは、を参照してください。 [Fastly 資格情報の取得](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#get-fastly-credentials) を参照してください。

### 1c. Fastly VCL スニペットのアップロード

詳しくは、 [Fastly への VCL のアップロード](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html) を参照してください。

以下の手順でも可能です [独自のカスタム VCL スニペットの作成と追加](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets.html).

### 1d. Fastly の DNS の設定


手順について詳しくは、この記事を参照してください。 [Fastly の設定](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-configuration.html#update-dns-configuration-with-development-settings) を参照してください。

### サポートナレッジベースの関連する Fastly 記事

* [Fastly キャッシュがクラウドで機能しない](/help/troubleshooting/miscellaneous/fastly-caching-is-not-working-on-magento-cloud.md)
* [クラウド上の Fastly キャッシュをパージする際にエラーが発生しました（パージリクエストが正常に処理されませんでした）](/help/troubleshooting/miscellaneous/error-purging-fastly-cache-on-cloud-the-purge-request-was-not-processed-successfully.md)

## 2.有効な SSL （TLS）証明書

問題：有効で機能する SSL 証明書がないと、ステージング環境のチェックアウトページで外部支払い方法をテストできません。

推奨事項 **:** ステージングまたはライブドメイン名の場合は、共有 SSL 証明書をリクエストします。

SSL 証明書については、こちらを参照してください [クイック FAQ](/help/announcements/adobe-commerce-announcements/magento-ssl-tls-certificate-requirements-and-clean-up.md) アドビのサポートナレッジベースの記事

## 3. 301 リダイレクトの設定とテスト

問題：301 リダイレクトが提供されないか、設定が不十分で、SEO ランキングと検索リストでストアがドロップする原因になります。

推奨事項 **:** 301 リダイレクトの設定とテストを慎重に行います。

古い web サイトから新しい web サイトに移行する場合は、以前にインデックスを作成した古いページから新しいストアの適切なページに顧客が 301 リダイレクトされます。例えば、次のようになります。

http://www.mywebsite.com/old-category-page.html **>** http://www.mywebsite.com/new-seo-friendly-category-page.html

**関連記事：**

* [routes.yaml 経由のリダイレクト](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/routes/redirects.html) を参照してください。
* [Cloud Console を使用したリダイレクト](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html) を参照してください。
* [URL リライト](https://experienceleague.adobe.com/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite.html) を参照してください。

## 4.アセットのパフォーマンス

問題：静的アセットの提供に時間がかかるので、サイトのパフォーマンスが低下します（読み込み時間が長くなる、マルチメディアコンテンツが表示されない、など）。 Web サイトの静的アセットには、CSS リソース、画像、ビデオ、添付ドキュメントなどがあります。 サイトのパフォーマンスの重要な要因は、コンテンツを整理し、提供する方法です。

推奨事項：パフォーマンス低下の考えられる原因を特定するには、次の使用を検討します [Adobe Commerce Performance Toolkit](https://github.com/magento/magento2/tree/2.3/setup/performance-toolkit) パフォーマンステスト用。 次のサードパーティツールも検討できます。

* [包囲](https://www.joedog.org/siege-home/): HTTP 負荷テストおよびベンチマークユーティリティ。基本認証、Cookie、HTTP、HTTPS および FTP プロトコルをサポートします。
* [Jmeter](https://jmeter.apache.org/)：評判の良い負荷テストおよびパフォーマンス測定ツール。 スパイクされたトラフィックのパフォーマンスを測定するのに役立ちます（例：フラッシュセールス）。
* [New Relic](https://support.newrelic.com/)：サイトのプロセスと領域を特定し、データ、クエリ、Redis などの送信に費やしたアクションごとの追跡時間でパフォーマンスの低下を引き起こします。
* [WebPageTest](https://www.webpagetest.org/) （無料）と [Pingdom](https://www.pingdom.com/) （有料）：サイトページのリアルタイム分析では、様々な接触チャネルの場所で時間を読み込みます。

次のことも検討してください。 [縮小](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/store-settings.html) （CSS、JavaScript、HTMLの場合）。

**関連記事：**

* [デプロイメントをテスト](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production.html) 開発者向けドキュメントを参照してください。
