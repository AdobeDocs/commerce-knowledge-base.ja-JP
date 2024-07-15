---
title: 過剰な Ajax リクエストによるパフォーマンスの問題
description: この記事では、過剰な Ajax リクエストによって発生するAdobe Commerceのパフォーマンスに関する既知の問題に対するパッチを提供します。 この問題は、Adobe Commerce 2.3.4 で修正されました。
exl-id: d9a69406-3970-4556-aa6a-1309b24366d8
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 過剰な Ajax リクエストによるパフォーマンスの問題

この記事では、過剰な Ajax リクエストによって発生するAdobe Commerceのパフォーマンスに関する既知の問題に対するパッチを提供します。 この問題は、Adobe Commerce 2.3.4 で修正されました。

## 問題

Adobe Commerceは、バナー情報とお客様の情報を取得するために、ストアフロントからサーバーに冗長な [Ajax リクエスト ](/help/troubleshooting/miscellaneous/high-throughput-ajax-requests-cause-poor-performance.md) を送信している可能性があります。 これらの Ajax 要求は、特に高負荷（大量および高トラフィック）の状況で、パフォーマンスに影響を与えます。 したがって、バナー機能を使用しない場合は、[Adobe Commerce Banner module の出力を完全に無効にする ](/help/troubleshooting/miscellaneous/disable-magento-banner-output-to-improve-site-performance.md) と、パッチを適用して顧客情報の取得を改善することをお勧めします。

## パッチ

パッチはこの記事に添付されています。 ダウンロードするには、記事の最後まで下にスクロールしてファイル名をクリックするか、次のリンクをクリックします。

[MDVA-24597\_EE\_2.2.9\_COMPOSER\_v1.patch のダウンロード](assets/MDVA-24597_EE_2.2.9_COMPOSER_v1.patch.zip)

### 互換性のあるAdobe Commerce バージョン

パッチは次の製品とバージョンで有効です。

* クラウドインフラストラクチャー 2.2.9 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.2.9

Adobe Commerceのバージョンが異なる場合は、最新の 2.3.x リリースにアップデートすることを検討してください。 現在、これが不可能な場合は、[Adobe Commerce サポートにお問い合わせ ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) いただき、ご使用のバージョンのパッチをリクエストしてください。

## パッチの適用方法

手順については、[Adobeが提供する Composer パッチの適用方法 ](/help/how-to/general/how-to-apply-a-composer-patch-provided-by-magento.md) を参照してください。

## 添付ファイル
