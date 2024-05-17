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

この記事では、次の場合にGraphQL リクエストの WAF をバイパスする方法について説明します。 [!DNL Fastly] WAF がGraphQL リクエストをブロックしています。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 原因：

GraphQL リクエストの性質上、リクエストが正と見なされないことをトリガーする反復文字が多数発生する場合があります。 [!DNL Fastly] WAF。

## 解決策

1. を介してカスタムスニペットを追加することで、これらのリクエストの WAF を回避します。 [!DNL Fastly] Magentoモジュール：

   タイプ：recv 優先度：15 コンテンツ：

   ```
   if( req.url.path ~ "^/graphql" ) {
       set req.http.bypasswaf = "1";
   }
   ```

1. クリックする **[!UICONTROL Upload VCL to Fastly]**.

## 関連資料

* [Web アプリケーションファイアウォール（WAF）](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service) （クラウドインフラストラクチャー上のCommerceに関するガイド）を参照してください。
* [カスタム VCL の概要](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-custom-snippets) （クラウドインフラストラクチャー上のCommerceに関するガイド）を参照してください。
