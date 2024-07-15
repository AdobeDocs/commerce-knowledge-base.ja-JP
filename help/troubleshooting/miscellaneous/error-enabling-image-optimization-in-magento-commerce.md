---
title: Adobe Commerceで画像の最適化を有効にする際にエラーが発生する
description: この記事では、Fastly の画像最適化（IO）がデフォルトで無効になっており、画像の最適化を有効にするために Fastly に連絡する通知が表示される場合の問題に対する解決策を説明します。 （Fastly Cloud Image Optimizer は、帯域幅を最適化した画像を提供することで画像の配信を高速化する、リアルタイムの画像操作および最適化サービスです）。
exl-id: 7b64c786-3c74-4642-b0d0-15b5648163a0
feature: Observability
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Adobe Commerceで画像の最適化を有効にする際にエラーが発生する

この記事では、Fastly の画像最適化（IO）がデフォルトで無効になっており、画像の最適化を有効にするために Fastly に連絡する通知が表示される場合の問題に対する解決策を説明します。 （Fastly Cloud Image Optimizer は、帯域幅を最適化した画像を提供することで画像の配信を高速化する、リアルタイムの画像操作および最適化サービスです）。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x

## 問題

Fastly 設定ページの Fastly IO スニペットの横には、現在の状態が「\_disabled \_with the following message below: Please contact your sales rep or send a email to `support@fastly.com` to request image optimization activation for your Fastly service」と表示されます。

## 原因：

サイトがまだ実稼働していない可能性があります。 Fastly データベースで運用を開始する際に、サイトをプリロードするプロセスがあります。

## 解決策

[ サポートチケット ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) を作成し、画像の最適化をリクエストします。
