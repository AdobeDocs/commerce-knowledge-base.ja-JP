---
title: GraphQL リクエストで WAF をバイパスする方法
description: この記事では、GraphQL リクエストで WAF をバイパスする方法について説明します。
feature: GraphQL
exl-id: 3a0f2c22-f976-4596-b6a9-4634be1ea4c3
source-git-commit: 2bec86818336a9ef4d8316e257a0ca4256cdd93c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# GraphQL リクエストで WAF をバイパスする方法

この記事では、[!DNL Fastly] WAF がGraphQL リクエストをブロックしている場合に、GraphQL リクエストの WAF をバイパスする方法について説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 原因：

GraphQL リクエストの性質上、[!DNL Fastly] WAF によるリクエストの偽陽性ブロッキングのトリガーになる可能性がある多くの繰り返し文字が存在する場合があります。

## 解決策

1. [!DNL Fastly] のMagentoモジュールを介してカスタムスニペットを追加することで、これらのリクエストに対する WAF を回避します。

   タイプ：recv
優先度：15
コンテンツ :

   ```
   if( req.url.path ~ "^/graphql" ) {
       set req.http.bypasswaf = "1";
   }
   ```

1. 「**[!UICONTROL Upload VCL to Fastly]**」をクリックします。

## 関連資料

* クラウドインフラストラクチャー上のCommerceにある [Web アプリケーションファイアウォール（WAF） ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service) に関するガイド。
* クラウドインフラストラクチャー上のCommerceにおける [ カスタム VCL の概要 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets) ガイド。
