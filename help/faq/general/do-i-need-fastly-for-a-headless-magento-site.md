---
title: ヘッドレスAdobe CommerceサイトにFastlyは必要ですか？
description: ヘッドレスAdobe CommerceサイトにFastlyは必要ですか？
exl-id: d7e07160-6a61-4c03-8f8c-4f879d86ea44
feature: Cache, GraphQL, Compliance
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# ヘッドレスAdobe CommerceサイトにFastlyは必要ですか？

>[!NOTE]
>
>すべてのお客様は、本番環境とステージング環境でFastlyを使用する必要があります。 Fastlyは、Adobe Commerce on Cloud インフラプロジェクトの一環として、フルページキャッシュ、画像の最適化、セキュリティサービス（DDoSおよびWAF）を提供するコンテンツ配信ネットワーク（CDN）です。 これらはAdobe Commerceソリューションのコアコンポーネントであり、パフォーマンスとセキュリティを向上させます。 これらの機能は、AdobeのPCI認定に含まれています。 これらのFastly サービスは、スターター環境、ステージングマスター、プロステージング環境、実稼動環境で設定する必要があります。 ヘッドレス実装でAdobe Commerceを使用している場合、パブリックインターネットからのすべてのAPI トラフィックはFastlyを通過する必要があります。GraphQLの応答をキャッシュするには、Fastlyを使用することを強くお勧めします。 開発者向けドキュメントでは、[GraphQL開発ガイド > Fastlyを使用したキャッシュ ](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly)を参照してください。

## **質問**

Adobe Commerceのヘッドレス実装を開発しています。 FastlyをCDN サービスとして使用する必要がありますか？

## **回答**

いえ、ご存じない方も。 このような場合、少なくとも開発の最初は、Fastlyを使用せずに済む可能性があります。

ヘッドレス CMSを導入する場合にのみ、対応が困難になる可能性があります。
詳しくは、開発者向けドキュメントの[Cloud for Adobe Commerce > Fastly](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly)を参照してください。

それでも、ほとんどの場合、SSL証明書を使用するにはFastlyが必要です。

クラウドインフラストラクチャ上のすべてのAdobe Commerceのお客様は、クラウドサブスクリプションプランの一部として、Fastlyから共有SSL証明書を取得します。 Fastlyに独自のSSL証明書を追加することは、別の高額な有料オプションです。 したがって、Fastlyを有効にし、少なくともヘッドレス Adobe Commerce web サイトを公開する前に、ステージング環境と実稼動環境でテストすることを強くお勧めします。

## 詳細

* [ ヘッドレス Web サイト：分離型アーキテクチャの大きなメリットは何ですか？](https://pantheon.io/blog/headless-websites-whats-big-deal-decoupled-architecture) 作成者：[Josh Koenig](https://pantheon.io/team/josh-koenig)
* [Fastly](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly)の詳細をご覧ください。
