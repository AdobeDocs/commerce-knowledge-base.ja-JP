---
title: デプロイメントが「リモートクラスターにアプリケーションをアップロードできません」エラーでスタックする
description: 「この記事では、デプロイメントが停止して、デプロイログに「エラー：アプリケーションをリモートクラスターにアップロードできません」というエラーメッセージが表示されるAdobe Commerceの問題の解決策について説明します。」
exl-id: 30f0ec31-db27-429c-b065-cf7770a72194
feature: Deploy
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# デプロイメントが「リモートクラスターにアプリケーションをアップロードできません」エラーでスタックする

この記事では、デプロイメントが停止して、デプロイログに「*エラー：リモートクラスターにアプリケーションをアップロードできません」というエラーメッセージが表示されるAdobe Commerceの問題の解決策を説明し* す。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

<u> 再現手順 </u>:

トリガーのデプロイメントを手動で行うか、環境の結合、プッシュまたは同期を実行して行います。

<u> 期待される結果 </u>:

デプロイメントが正常に完了しました。

<u> 実際の結果 </u>:

デプロイメントが停止し、Cloud UI のデプロイメントエラーログに、次のエラーメッセージが表示されます。*「エラー：リモートクラスターにアプリケーションをアップロードできません」がデプロイログで見つかりました。デプロイメントに失敗すると、サイトに「503 最初のバイトのタイムアウト」というエラーが表示される場合があり* す。

## 原因：

この問題は、利用可能なストレージが停止したために発生します。

## 解決策

ログディレクトリのクリーニングやディスク容量の増加を検討できます。

クリーンアップ対象と見なされるディレクトリ：

* `var/log`
* `var/report`
* `var/debug/`
* `var`

Adobe Commerce on cloud infrastructure スタータープランアーキテクチャを使用している場合にディスク容量を増やす方法について詳しくは、サポートナレッジベースの [ クラウド上の統合環境のディスク容量の増加 ](/help/how-to/general/increase-disk-space-for-integration-environment-on-cloud.md) を参照してください。 同じ手順を使用して、Adobe Commerce on cloud infrastructure Pro プランアーキテクチャの統合環境のスペースを増やすことができます。 プロ実稼働/ステージングの場合は、[Adobe Commerce サポートにチケットを提出 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket-Submit-a-support-ticket) し、ディスク容量の増加をリクエストする必要があります。 ただし、通常は、Adobe Commerceがこれらのパラメーターをモニタリングし、アラートを送信したり、契約に従ってアクションを実行したりするので、Pro プランのステージング/実稼動で対処する必要はありません。
