---
title: Adobe Commerce ストアフロントでログアウトするか、カートのコンテンツを失う
description: この記事では、支払いやその他のサードパーティサービス（session cookie "gets lost"）からAdobe Commerce ストアにリダイレクトされた後、ストアフロントのショッピングカートからログアウトしたり、商品を失ったりする問題の解決策と回避策について説明します。
exl-id: 9175570c-b06c-4a65-b8ca-7a12ff266afb
feature: Orders, Page Content, Shopping Cart, Storefront
role: Admin
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Adobe Commerce ストアフロントでログアウトするか、カートのコンテンツを失う

この記事では、お客様が支払いやその他のサードパーティサービスからAdobe Commerce ストアにリダイレクトされた後、ストアフロントのショッピングカートからログアウトまたはアイテムを失う問題の解決策を提供します（session cookie &quot;gets lost&quot;）。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)
* クラウドインフラストラクチャ上のAdobe Commerce、[&#x200B; サポートされているすべてのバージョン &#x200B;](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)

## イシュー

<u>再生する手順：</u>

1. 顧客はストアフロントのカートに商品を追加して、チェックアウトに進みます。
1. お客様は、支払い/配送またはその他の情報/サービスのために、サードパーティサイトにリダイレクトされます。
1. お客様が店舗にリダイレクトされます。

<u>実際の結果：</u>

お客様が、空のショッピングカートまたは空白のページにリダイレクトしました。

<u>期待される結果：</u>

お客様は、チェックアウトデータと進行状況を失うことなく、成功した支払いページ（またはその他の成功ページ）にリダイレクトされました。

## 原因

SameSite cookie属性が&#x200B;*Lax*&#x200B;に設定されているか、指定されていません（これは&#x200B;*Lax*&#x200B;に設定されているとして扱われます）。 `SameSite` = *Lax*&#x200B;を使用すると、Cookieを`POST`要求を介して外部URLに転送できなくなります。

## Solution

この問題を解決するには、サードパーティのサービスプロバイダーに連絡し、開発者に対して統合の更新を依頼してCookie パラメーターを設定します。

## 関連トピックス

[Chrome SameSite アップデート](https://www.chromestatus.com/feature/5088147346030592)
