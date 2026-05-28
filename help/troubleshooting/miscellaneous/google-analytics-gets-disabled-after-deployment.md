---
title: デプロイメント後にGoogle Analyticsが無効になる
description: ここでは、デプロイメント時にGoogle Analyticsで発生する可能性のある一般的な問題の解決策について説明します。
exl-id: ecf6a277-2dfa-45cf-b86f-9a27f39017f4
feature: Build, Deploy, Variables
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

Google Analyticsを常に有効にする場合は、開発者ドキュメントの[変数のデプロイ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#enable_google_analytics)で説明されているように、デプロイ変数`ENABLE_GOOGLE_ANALYTICS = true`を設定します。

>[!NOTE]
>
>私たちは、この記事には、一部の人が人種差別的、性差別的、または抑圧的であると感じる可能性があり、読者が傷つけられ、トラウマを負わされ、または歓迎されないと感じる可能性がある、業界標準のソフトウェア用語がまだ含まれている可能性があることを認識しています。 Adobeでは、コード、ドキュメント、ユーザーエクスペリエンスからこれらの用語を削除しようと取り組んでいます。
