---
title: サンドボックス環境でクレジットカードの支払いが失敗しました
description: この記事では、PayPal API を使用したサンドボックス環境でテストクレジットカードが失敗する理由を説明します。
exl-id: 65fd08e0-eefc-47f3-8964-bef3610e6182
feature: Orders, Payments
role: Developer
source-git-commit: 35d4f2130d0ec71f71f5f20aa8a7c76207e7a35a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# サンドボックス環境でクレジットカードの支払いが失敗しました

この記事では、PayPal API を使用したサンドボックス環境でテストクレジットカードが失敗する理由を説明します。

## 影響を受ける製品とバージョン


* Adobe Commerce 2.4.0 ～ 2.4.4、すべてのデプロイメントオプション、[ 支払いサービス ](https://marketplace.magento.com/magento-payment-services.html)

## 問題

PayPal からテスト用の Visa クレジットカード `4111 1111 1111 1111` ードを使用する場合、PayPal の不正ポリシーが原因で次のエラーで失敗することがあります。

```bash
Error happened when processing the request. Please try again later.
```

## 原因：

このエラーは、PayPal が不正行為のために特定のテストクレジットカード番号にフラグを立てるときに表示されます。 これは、PayPal API を使用してテストする世界中の誰もが使用するテスト用クレジットカード番号であるためです。

## 解決策

別のテストクレジットカードを使用します。 モッククレジットカードを生成するために、テストに使用できます。

1. PayPal 開発者ポータル [ クレジットカード生成 ](https://developer.paypal.com/developer/creditCardGenerator/) ページに移動します。
1. PayPal 開発者ポータルダッシュボードにログインします。
1. テストクレジットカードを生成します。
