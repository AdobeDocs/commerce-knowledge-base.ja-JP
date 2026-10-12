---
title: メンテナンスモードのサイトですが、顧客が利用できます
description: この記事では、メンテナンスモードが有効になっている場合（Adobe Commerce オンクラウドインフラストラクチャの問題）の修正点を説明しますが、ストアフロントは引き続きお客様が利用できます。
exl-id: 61b81fbd-a382-44b5-94e9-5b6d72f11349
feature: Cache
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
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
source-wordcount: '159'
ht-degree: 0%
---
# メンテナンスモードのサイトですが、顧客が利用できます

この記事では、メンテナンスモードが有効になっている場合（Adobe Commerce オンクラウドインフラストラクチャの問題）の修正点を説明しますが、ストアフロントは引き続きお客様が利用できます。

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure （すべてのバージョン）

## イシュー

<u>再生する手順：</u>

1. サイトのメンテナンスモードを有効にします。
1. ストアフロントに移動します。

<u>期待される結果：</u>

保守ページが表示されます。

<u>実際の結果：</u>

ストアフロントページは通常どおり表示されます。

## 原因

ページは引き続きキャッシュされるため、メンテナンスページは表示されません。

## メンテナンスモードにもかかわらずサイトを表示するソリューション

1. 環境にSSHで接続します。
1. `php bin/magento cache:clean` コマンドを実行します。

## 関連トピックス

[&#x200B; メンテナンスモードを有効または無効にします](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/maintenance-mode)。詳しくは、開発者向けドキュメントを参照してください。
