---
title: Payment Services のインストールのトラブルシューティング
description: この記事では、支払いサービスのインストール中に発生する可能性のあるエラーについて説明し、インストールを完了するためにこれらのエラーを修正するソリューションを提供します。
exl-id: 0aef7482-8834-400e-85b9-d3d3eb0ab76e
feature: Install, Orders, Payments, Saas
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Payment Services のインストールのトラブルシューティング

この記事では、支払いサービスのインストール中に発生する可能性のあるエラーについて説明し、インストールを完了するためにこれらのエラーを修正するソリューションを提供します。

## 影響を受ける製品とバージョン

* [ 支払いサービス ](https://marketplace.magento.com/magento-payment-services.html) は、Adobe Commerce バージョン 2.4.0 から 2.4.4 と互換性を持つようになりました。

## 問題 – コンポーザーのキーが正しくありません

Payment Services 拡張機能をインストールすると、インストール時に間違った Composer キーを使用したことを示すエラーメッセージが表示される場合があります。

<u> 再現手順 </u>:

1. [ 支払いサービスのインストール ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html?lang=ja) を試みます。
1. 次のエラーが表示されます。

   *magento/payment-services パッケージの一致するバージョンが見つかりませんでした。 パッケージのスペル、バージョンの制約、およびパッケージが最小安定性（stable）に一致する安定性で使用可能であることを確認します。*

<u> 期待される結果 </u>:

アドビの開発者向けドキュメントの以下の [ インストール手順 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html?lang=ja) に従って、支払いサービスを正常にインストールできます。

<u> 実際の結果 </u>:

インストール中に、インストール中に正しい Composer キーを使用しなかったことを示すエラーメッセージが表示されます。

### 原因：

インストール中に間違った Composer キーが使用されました。

### 解決策

Payment Services の登録時に使用した [Composer キーがMagentoID にリンクされている ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html?lang=ja#incorrect-composer-keys) ことを確認します。

## 問題 – 複数のインスタンスで同じデータスペースを使用する

それぞれに支払いサービスを含むマルチ環境の設定を実行する。

### 解決策

同じ API キーを複数のインスタンスで使用できますが、各インスタンスで独自の SaaS データ領域を使用する必要があります。

SaaS プロジェクトを作成すると、CommerceはCommerce ライセンスに応じて 1 つ以上の SaaS データスペースを生成します。

* Adobe Commerce – 実稼動データスペース 1 つ、テスト用データスペース 2 つ
* Magento Open Source - 1 つの実稼動データスペースで、テスト用のデータスペースはない

[Commerce API キーと秘密鍵 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html?lang=ja#obtain-api-credentials) の手順に従って、支払いサービス拡張機能を正常に設定します。

## 問題 – PHP 用のメモリが不足しています

Payment Services 拡張機能をインストールすると、PHP に十分なメモリがないことを示すエラーメッセージが表示される場合があります。

<u> 再現手順 </u>:

1. [ 支払いサービスのインストール ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html?lang=ja) を試みます。
1. 次のエラーまたは同様のエラーが表示されます。

   *致命的なエラー：52 行目のphar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.phpで 2146435072 バイトのメモリ サイズが使い果たされました（4096 バイトの割り当てを試みました）*

<u> 期待される結果 </u>:

アドビの開発者向けドキュメントの以下の [ インストール手順 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html?lang=ja) に従って、支払いサービスを正常にインストールできます。

<u> 実際の結果 </u>:

インストール中に、PHP 用のメモリが不足していることを示すエラーメッセージが表示されます。

### 原因：

お使いの環境の PHP の上限が十分なしきい値に設定されていません。

### 解決策

[PHP のメモリの上限を増やす ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/install.html?lang=ja#not-enough-memory-for-php) を使用している環境で `php.ini` ます。
