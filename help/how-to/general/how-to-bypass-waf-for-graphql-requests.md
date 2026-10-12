---
title: GraphQL リクエストに対するWAFのバイパス方法
description: この記事では、GraphQL リクエストに対してWAFをバイパスする方法について説明します。
feature: GraphQL
exl-id: 3a0f2c22-f976-4596-b6a9-4634be1ea4c3
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
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

1. [!DNL Fastly] Magento モジュールを通じてカスタムスニペットを追加することで、これらのリクエストに対するWAFをバイパスします。

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
