---
title: メンテナンスモードになっているが、顧客が使用できるサイト
description: この記事では、メンテナンスモードが有効になっている（クラウドインフラストラクチャ上のAdobe Commerceの問題）が、お客様は引き続きストアフロントを使用できる場合の解決策を提供します。
exl-id: 61b81fbd-a382-44b5-94e9-5b6d72f11349
feature: Cache
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# メンテナンスモードになっているが、顧客が使用できるサイト

この記事では、メンテナンスモードが有効になっている（クラウドインフラストラクチャ上のAdobe Commerceの問題）が、お客様は引き続きストアフロントを使用できる場合の解決策を提供します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

<u> 再現手順：</u>

1. サイトのメンテナンスモードを有効にします。
1. ストアフロントに移動します。

<u> 期待される結果：</u>

メンテナンスページが表示されます。

<u> 実際の結果：</u>

ストアフロントページは通常どおり表示されます。

## 原因：

ページは引き続きキャッシュされるので、メンテナンスページは表示されません。

## メンテナンスモードであるにもかかわらず、サイトに対して可視のソリューション

1. 環境に SSH で接続します。
1. `php bin/magento cache:clean` コマンドを実行します。

## 関連資料

開発者向けドキュメントの [&#x200B; メンテナンスモードの有効化または無効化 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/maintenance-mode) を参照してください。
