---
title: GraphQL リクエストに対するWAFのバイパス方法
description: この記事では、GraphQL リクエストに対してWAFをバイパスする方法について説明します。
feature: GraphQL
exl-id: 3a0f2c22-f976-4596-b6a9-4634be1ea4c3
source-git-commit: 2bec86818336a9ef4d8316e257a0ca4256cdd93c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# GraphQL リクエストに対するWAFのバイパス方法

この記事では、[!DNL Fastly] WAFがGraphQL リクエストをブロックしている場合に、GraphQL リクエストに対してWAFをバイパスする方法について説明します。

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure （すべてのバージョン）

## 原因

GraphQL リクエストの固有の性質により、[!DNL Fastly] WAFによるリクエストの偽陽性ブロックをトリガーする可能性のある繰り返し文字が大量に存在する可能性があります。

## Solution

1. [!DNL Fastly] Magento モジュールを使用してカスタムスニペットを追加することで、これらのリクエストに対するWAFをバイパスします。

   タイプ：recv
   優先度：15
   コンテンツ：

   ```
   if( req.url.path ~ "^/graphql" ) {
       set req.http.bypasswaf = "1";
   }
   ```

1. **[!UICONTROL Upload VCL to Fastly]**&#x200B;をクリックします。

## 関連トピックス

* Commerce on Cloud Infrastructure ガイドの[Web Application Firewall （WAF） &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service)。
* Commerce Cloud Infrastructure版の[&#x200B; カスタム VCL](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets)の概要ガイド。
