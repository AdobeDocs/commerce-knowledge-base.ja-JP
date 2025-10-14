---
title: 書き出しストレージがほとんどいっぱいであることを示すメール
description: この記事では、書き出しストレージがほぼいっぱいであることを示すメールが届く問題の解決策を説明します。
feature: Cloud, Storage, Media
role: Developer
exl-id: 7dae295c-919c-46c5-bf63-7d3467c2e07f
source-git-commit: 89f985b832545f1fbccf94aac1d60f1e767b5bc4
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# ストレージがほぼいっぱいであることを示すメール

この記事では、書き出しストレージがほぼいっぱいであることを示すメールが届く問題の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

次の内容のメールが届きますが、*exports* フォルダーが見つかりません。

*監視により、クラスター XXX の「エクスポート」ストレージがおよそ「85%」いっぱいであることが検出されました。*
*必要に応じて、使用状況を確認したり、クリーンアップを実行したり、アップサイズをリクエストしたりします。*
*また、ストレージが重大しきい値レベルに達すると、自動的にアップサイズが試行されることに注意してください。*

## 原因：

メールは、**書き出し** ストレージを参照しています。これは、ファイルやメディアに割り当てられたディスクの量であり、*書き出し* という特定のフォルダーではありません。

## 解決策

環境でのファイルの使用状況を確認する必要があります。 次のコマンドを実行して、既存の使用方法を取得します。

`df -h |grep data`

ファイルのストレージがいっぱいになる可能性が高い一般的な場所は、*pub/media/catalog/product/cache* または *var/log* フォルダーです。 ファイルが使用しているディスク領域を調べるには、次のコマンドを適切なパス */path/to/folder* で実行します。

`du -shc` */path/to/folder*

メディアディスク使用量が合計ディスク容量の大きな割合を占める場合は、[Fastly Deep Image Optimization](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization#deep-image-optimization) を有効にしてから、サーバー上の *pub/media/catalog/product/cache* フォルダーのファイルを手動で削除することを検討してください。

## 関連資料

サポートナレッジベースで [&#x200B; 専用クラスターを確認 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space#check-dedicated-clusters) してください。
