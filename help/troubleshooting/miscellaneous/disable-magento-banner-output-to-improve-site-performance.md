---
title: サイトのパフォーマンスを向上させるために、Adobe Commerce バナーの出力を無効にします
description: この記事では、サイトパフォーマンスの低下に対する修正を示します。 「Banner_Banner」モジュールが有効になっているものの使用されていないことが原因で、サイトのMagentoが低下している可能性があります。 モジュール出力を無効にすると、サイトのパフォーマンスが向上する可能性があります。 解決手順については、記事を確認してください。
exl-id: 90a8bd21-1f2c-4cfe-8213-17f877e20de8
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# サイトのパフォーマンスを向上させるために、Adobe Commerce バナーの出力を無効にします

この記事では、サイトパフォーマンスの低下に対する修正を示します。 サイトパフォーマンスの低下は、次の原因が原因で発生する可能性があります `Magento_Banner` モジュールは有効になっていますが、使用されていません。 モジュール出力を無効にすると、サイトのパフォーマンスが向上する可能性があります。 解決手順については、記事を確認してください。

>[!NOTE]
>
>Adobe Commerce Banner 機能を使用する場合は、 [スループットの高いAJAX リクエストが原因で、パフォーマンスが低下する](/help/troubleshooting/miscellaneous/high-throughput-ajax-requests-cause-poor-performance.md) 過剰な Ajax リクエストによって発生するパフォーマンスの問題を回避する方法に関する推奨事項については、サポートナレッジベースの記事を参照してください。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce v.2.x.x
* Adobe Commerce オンプレミス v.2.2.x および 2.3.x

## 問題

この `Magento_Banner` モジュールは有効になっていますが、使用されていません。

その場合は、次の手順を実行します。

クラウドインフラストラクチャー 2.2.x 上のAdobe Commerceの場合：

1. Commerce Admin にログインします。
1. に移動します。 **コンテンツ** > *要素* > **バナー**.
1. このページに表示されるグリッドが空の場合は、バナーはありません。

が表示されない場合、 **バナー** オプション： **コンテンツ** > *要素*&#x200B;したがって、これは該当せず、この記事からの推奨事項は適用できません。

Cloud infrastructure 2.3.x 上のAdobe Commerceの場合（機能は次のとおりです [v 2.3.x での名前の変更](https://devdocs.magento.com/guides/v2.3/release-notes/ReleaseNotes2.3.0Commerce.html#banner-now-dynamic-block)）:

1. Commerce Admin にログインします。
1. に移動します。 **コンテンツ** > *要素 >*  **ダイナミック ブロック**.
1. このページに表示されるグリッドが空の場合は、ダイナミック ブロック（バナー）はありません。

が表示されない場合、 **ダイナミック ブロック** オプション： **コンテンツ** > *要素*&#x200B;したがって、これは該当せず、この記事からの推奨事項は適用できません。

## 原因：

いつ `Magento_Banner` モジュールを有効にすると、Adobe Commerceはバナー情報を取得するための Ajax リクエストをストアフロントからサーバーに送信します。 これらの Ajax 要求は、特に高負荷（大量および高トラフィック）の状況で、パフォーマンスに影響を与えます。 機能を使用しない場合は、モジュール出力を無効にすることをお勧めします。 依存関係の問題があるので、モジュールを無効にしないことをお勧めします。

## 解決策

>[!WARNING]
>
>の変更をテストすることを強くお勧めします。 [ステージング/統合環境](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) まず、実稼動環境に適用する前に以下を行います。 また、操作の前に最新のバックアップを取ることをお勧めします。

1. を無効にする `Magento_Banner` モジュール出力（「」を参照） [モジュール出力を無効にする](https://devdocs.magento.com/guides/v2.3/config-guide/config/disable-module-output.html) 開発者向けドキュメントを参照してください。 使用する必要があるモジュール名は次のとおりです。 `Magento_Banner`.
1. コードのデプロイ。 クラウドインフラストラクチャー上のAdobe Commerceの場合は、の説明に従って、をデプロイします。 [ストアのデプロイ](https://devdocs.magento.com/guides/v2.3/cloud/live/stage-prod-live.html) 開発者向けドキュメントの記事。
