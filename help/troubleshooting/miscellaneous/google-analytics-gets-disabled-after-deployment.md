---
title: デプロイ後にGoogle Analyticsが無効になる
description: ここでは、のデプロイ中にGoogle Analyticsが発生する可能性のある、一般的な問題の解決策について説明します。
exl-id: ecf6a277-2dfa-45cf-b86f-9a27f39017f4
feature: Build, Deploy, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# デプロイ後にGoogle Analyticsが無効になる

ここでは、のデプロイ中にGoogle Analyticsが発生する可能性のある、一般的な問題の解決策について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

環境全体にコードをデプロイする場合は、ビルドスクリプトとデプロイスクリプトによって `master/production/staging` ブランチがデプロイされ、Google Analyticsが有効に保たれるかどうかが検証されます。 マスターの開発（または子）ブランチを開発環境（Integration）にデプロイする場合、デプロイスクリプトでGoogle Analyticsが無効になります。

## 原因：

これは、開発者データとインタラクションが、Google Analyticsに送信されたり、トラッキングされたりしないようにするための機能です。

## 解決策

変数を常に有効にする場合は、開発者向けドキュメントの [Google Analyticsのデプロイ ](https://devdocs.magento.com/guides/v2.3/cloud/env/variables-deploy.html#enable_google_analytics) の説明に従って、デプロイ変数を `ENABLE_GOOGLE_ANALYTICS = true` 定します。

>[!NOTE]
>
>この記事には、人種差別的、性差別的、または抑圧的と思われる業界標準のソフトウェア用語が依然として含まれており、読者が苦痛を感じたり、トラウマを抱いたり、歓迎されないと感じたりする場合があることを認識しています。 Adobeでは、これらの用語をアドビのコード、ドキュメントおよびユーザーエクスペリエンスから削除するよう取り組んでいます。
