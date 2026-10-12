---
title: Github トークンの問題とコンポーザーのキー手順
description: この記事では、古いComposer キーが原因で発生するGithub トークンの失敗に関連するデプロイメントの失敗に関する問題の解決策を提供します。
exl-id: 202cb936-f9ba-49ea-bf0a-6e6994d2337a
feature: Identity Management
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: 23bc8570-95c6-5ef5-a563-2e4a4e6b4853
    internal-label: Identity Management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%
---
# Github トークンの問題とコンポーザーのキー手順

この記事では、古いComposer キーが原因で発生するGithub トークンの失敗に関連するデプロイメントの失敗に関する問題の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)
* Composer バージョン 1.10.20以前

>[!NOTE]
>
>Adobe Commerce オンプレミスのマーチャントは、Gitによって導入されたトークン形式の変更により、Composer バージョン 1.10.21以降を使用していることをホストプロバイダーに確認する必要があります。

## イシュー

デプロイメントが失敗し、デプロイメントログには次のような情報が含まれます。

*致命的なエラー：Uncaught UnexpectedValueException: github.comのgithub oauth トークンに、/app/vendor/composer/composer/src/Composer/IO/BaseIO.php:129*&#x200B;の「ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx」という無効な文字が含まれています

## 原因

古いComposer キーは、Github トークンのエラーを引き起こし、デプロイメントが失敗します。

## Solution

この問題を解決するには、コンポーザーのバージョンを1.10.22に更新してください。

1. ローカル環境で`composer require “composer/composer”:”>1.10.21`を実行します。
1. これにより、Composer パッケージバージョンの要件が追加されます。 ロックファイル - `composer/composer` バージョンは1.0.22以降である必要があります。
1. `composer.json`と`composer.lock`をコミットし、デプロイメントをプッシュします。

この方法が機能しない場合は、[&#x200B; サポートチケットを送信してください](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket)。

## 関連トピックス

* [Githubのブログ：GitHubの新しい認証トークン形式の背景](https://github.blog/2021-04-05-behind-githubs-new-authentication-token-formats/)
* [InfoQ.com ニュース記事：GitHubが識別可能性、シークレットスキャン、エントロピーを改善するためにトークン形式を変更](https://www.infoq.com/news/2021/04/github-new-token-format/)
