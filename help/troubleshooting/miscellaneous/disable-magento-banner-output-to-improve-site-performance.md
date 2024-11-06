---
title: サイトのパフォーマンスを向上させるために、Adobe Commerce バナーの出力を無効にします
description: この記事では、サイトパフォーマンスの低下に対する修正を示します。 「Banner_Banner」モジュールが有効になっているものの使用されていないことが原因で、サイトのMagentoが低下している可能性があります。 モジュール出力を無効にすると、サイトのパフォーマンスが向上する可能性があります。 解決手順については、記事を確認してください。
exl-id: 90a8bd21-1f2c-4cfe-8213-17f877e20de8
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# サイトのパフォーマンスを向上させるために、Adobe Commerce バナーの出力を無効にします

この記事では、サイトパフォーマンスの低下に対する修正を示します。 `Magento_Banner` モジュールが有効になっているのに使用されていないことが原因で、サイトのパフォーマンスが低下する可能性があります。 モジュール出力を無効にすると、サイトのパフォーマンスが向上する可能性があります。 解決手順については、記事を確認してください。

>[!NOTE]
>
>Adobe Commerce Banner 機能を使用する場合は、サポートナレッジベースの [ 高スループットのAJAX リクエストがパフォーマンスを低下させる ](/help/troubleshooting/miscellaneous/high-throughput-ajax-requests-cause-poor-performance.md) 記事で、過剰な Ajax リクエストによって発生するパフォーマンスの問題を回避する方法を参照してください。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce v.2.x.x
* Adobe Commerce オンプレミス v.2.2.x および 2.3.x

## 問題

`Magento_Banner` モジュールは有効になっていますが、使用されていません。

その場合は、次の手順を実行します。

クラウドインフラストラクチャー 2.2.x 上のAdobe Commerceの場合：

1. Commerce Admin にログインします。
1. **コンテンツ**/*要素*/**バナー** に移動します。
1. このページに表示されるグリッドが空の場合は、バナーはありません。

**コンテンツ**/*要素* の下に「**バナー**」オプションが表示されない場合は、そのようにはならず、この記事の推奨事項は適用できません。

Cloud infrastructure 2.3.x 上のAdobe Commerceの場合（機能は [v 2.3.x で名前が変更されました ](https://commerce-docs.github.io/devdocs-archive/2.3/guides/v2.3/release-notes/ReleaseNotes2.3.0Commerce.html#banner-now-dynamic-block)）:

1. Commerce Admin にログインします。
1. **コンテンツ**/*要素/* **動的ブロック** に移動します。
1. このページに表示されるグリッドが空の場合は、ダイナミック ブロック（バナー）はありません。

**コンテンツ**/*要素* の下に **動的ブロック** オプションが表示されない場合、これは該当せず、この記事の推奨事項は適用できません。

## 原因：

`Magento_Banner` モジュールが有効な場合、Adobe Commerceはバナー情報を取得するための Ajax リクエストをストアフロントからサーバーに送信します。 これらの Ajax 要求は、特に高負荷（大量および高トラフィック）の状況で、パフォーマンスに影響を与えます。 機能を使用しない場合は、モジュール出力を無効にすることをお勧めします。 依存関係の問題があるので、モジュールを無効にしないことをお勧めします。

## 解決策

>[!WARNING]
>
>実稼動環境に適用する前に、まず [ ステージング/統合環境 ](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) で変更をテストすることを強くお勧めします。 また、操作の前に最新のバックアップを取ることをお勧めします。

1. 開発者向けドキュメントの [ モジュール出力の無効化 ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/disable-module-output) の説明に従って、`Magento_Banner` モジュール出力を無効にします。 使用する必要があるモジュール名は `Magento_Banner` です。
1. コードのデプロイ。 クラウドインフラストラクチャー上のAdobe Commerceの場合は、開発者向けドキュメントの [ ストアのデプロイ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) の記事の説明に従ってデプロイします。
