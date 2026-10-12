---
title: デプロイメント後にGoogle Analyticsが無効になる
description: ここでは、デプロイメント時にGoogle Analyticsで発生する可能性のある一般的な問題の解決策について説明します。
exl-id: ecf6a277-2dfa-45cf-b86f-9a27f39017f4
feature: Build, Deploy, Variables
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
subfeature_v2:
  - id: adedf3b3-e153-47a3-ae73-b5d65067b544
    internal-label: Build system
  - id: 2191e157-828a-5358-ad69-ebcaa8402915
    internal-label: Variables
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%
---
# デプロイメント後にGoogle Analyticsが無効になる

ここでは、デプロイメント時にGoogle Analyticsで発生する可能性のある一般的な問題の解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerceオンクラウドインフラストラクチャ（全バージョン）

## イシュー

環境にコードをデプロイする際に、ビルドスクリプトとデプロイスクリプトによって、`master/production/staging` ブランチがデプロイされ、Google Analyticsが有効に保たれることが確認されます。 マスターの開発（または子）ブランチをデベロッパー環境（統合）にデプロイする場合、デプロイスクリプトはGoogle Analyticsを無効にします。

## 原因

これは、開発者データとインタラクションがGoogle Analyticsに送信されたり、追跡されたりしないようにするための機能です。

## Solution

Google Analyticsを常に有効にする場合は、開発者ドキュメントの[変数のデプロイ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#enable_google_analytics)で説明されているように、デプロイ変数`ENABLE_GOOGLE_ANALYTICS = true`を設定します。

>[!NOTE]
>
>私たちは、この記事には、一部の人が人種差別的、性差別的、または抑圧的であると感じる可能性があり、読者が傷つけられ、トラウマを負わされ、または歓迎されないと感じる可能性がある、業界標準のソフトウェア用語がまだ含まれている可能性があることを認識しています。 Adobeでは、コード、ドキュメント、ユーザーエクスペリエンスからこれらの用語を削除しようと取り組んでいます。
