---
title: Github トークンの問題と Composer の主要手順
description: この記事では、古い Composer キーが原因で発生した Github トークンの失敗に関連するデプロイメントの失敗の問題に対する解決策を提供します。
exl-id: 202cb936-f9ba-49ea-bf0a-6e6994d2337a
feature: Identity Management
role: Developer
source-git-commit: da2df5fc4ab6cc10d86af806045ee884b01f291d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Github トークンの問題と Composer の主要手順

この記事では、古い Composer キーが原因で発生した Github トークンの失敗に関連するデプロイメントの失敗の問題に対する解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce[&#x200B; サポート対象のすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)
* Composer バージョン 1.10.20 以前

>[!NOTE]
>
>Adobe Commerce オンプレミスのマーチャントは、Git によって導入されたトークン形式の変更により、Composer バージョン 1.10.21 以降を使用していることをホスト プロバイダーに確認する必要があります。

## 問題

デプロイメントが失敗し、デプロイメントログに次のような情報が含まれている場合：

*致命的なエラー：見つからなかった予期しない ValueException: github.com/app/vendor/composer/composer/src/Composer/IO/BaseIO.phpの github OAuth トークンに無効な文字：「ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx」が含まれている:129*

## 原因：

Composer キーが古いと、Github トークンでエラーが発生し、デプロイメントが失敗します。

## 解決策

この問題を解決するには、Composer のバージョンを 1.10.22 にアップデートしてください。

1. ローカル環境で、`composer require “composer/composer”:”>1.10.21` を実行します。
1. これにより、その Composer パッケージ バージョンの要件が追加されます。 ロックファイルを確認します。`composer/composer` のバージョンは 1.0.22 以降である必要があります。
1. `composer.json` および `composer.lock` をコミットし、デプロイメントをプッシュします。

この方法が機能しない場合は、[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) してください。

## 関連資料

* [Github ブログ：GitHub の新しい認証トークン形式の背後 &#x200B;](https://github.blog/2021-04-05-behind-githubs-new-authentication-token-formats/)
* [InfoQ.com ニュース記事：GitHub でトークン形式が変更され、識別性、秘密鍵スキャンおよびエントロピーが向上 &#x200B;](https://www.infoq.com/news/2021/04/github-new-token-format/)
