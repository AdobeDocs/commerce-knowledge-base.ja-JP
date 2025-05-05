---
title: ヘッドレス Adobe Commerce サイトには Fastly は必要ですか？
description: ヘッドレス Adobe Commerce サイトには Fastly は必要ですか？
exl-id: d7e07160-6a61-4c03-8f8c-4f879d86ea44
feature: Cache, GraphQL, Compliance
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# ヘッドレス Adobe Commerce サイトには Fastly は必要ですか？

>[!NOTE]
>
>すべてのお客様は、実稼動環境とステージング環境に Fastly を使用する必要があります。 Fastly は、フルページキャッシュ、画像の最適化、セキュリティサービス（DDoS およびWAF）をクラウドインフラストラクチャプロジェクト上のAdobe Commerceの一部として提供するコンテンツ配信ネットワーク（CDN）です。 これらは、Adobe Commerce ソリューションのコアコンポーネントであり、パフォーマンスとセキュリティを向上させます。 これらの機能は、Adobeの PCI コンプライアンスの一部です。 これらの Fastly サービスは、スターター環境、ステージング環境、ステージング環境、実稼動マスターでセットアップする必要があります。 ヘッドレスデプロイメントでAdobe Commerceを使用している場合、パブリックインターネットからのすべての API トラフィックは Fastly を経由する必要があります。Fastly を使用してGraphQLの応答をキャッシュすることを強くお勧めします。 開発者向けドキュメントの [GraphQL開発者ガイド > Fastly でのキャッシュ ](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) を参照してください。

## **質問**

Adobe Commerceのヘッドレス実装を開発中です。 それでも、Fastly を CDN サービスとして使用する必要がありますか？

## **回答**

いいえ、言ってません。この場合、少なくとも開発の最初は、Fastly の使用をスキップすることができます。

有効にしたくない状況は、ヘッドレスデプロイメントの場合のみです。
開発者向けドキュメントの [Cloud for Adobe Commerce > Fastly](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly) を参照してください。

それでも、ほとんどの場合、SSL 証明書を使用するには Fastly が必要になります。

クラウドインフラストラクチャー上のすべてのAdobe Commerceのお客様は、クラウドサブスクリプションプランの一環として、Fastly から共有 SSL 証明書を取得します。 Fastly への独自の SSL 証明書の追加は、別の、かなり高価な有料オプションです。 したがって、ヘッドレス Adobe Commerceの Web サイトであっても、Fastly を有効にし、少なくともステージング環境と実稼動環境で運用開始前にテストすることを強くお勧めします。

## 詳細情報

* [&#128279;](https://pantheon.io/blog/headless-websites-whats-big-deal-decoupled-architecture) ヘッドレス Web サイト：分離されたアーキテクチャに関する大きな問題は何ですか？[Josh Koenig](https://pantheon.io/team/josh-koenig) による 。
* [Fastly](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly) については、開発者向けドキュメントを参照してください。
