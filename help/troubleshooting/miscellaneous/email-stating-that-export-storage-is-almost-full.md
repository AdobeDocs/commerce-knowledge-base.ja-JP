---
title: 「書き出しストレージがほぼ満杯であることを示すメール」
description: この記事では、書き出しストレージがほぼいっぱいであることを示すメールが届く問題の解決策を説明します。
feature: Cloud, Storage, Media
role: Developer
source-git-commit: 8f783cb4245911bded5e9946917e2f2c3e78a705
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# ストレージがほぼいっぱいであることを示すメール

この記事では、書き出しストレージがほぼいっぱいであることを示すメールが届く問題の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

次の内容のメールが届きますが、が見つかりません *エクスポート* フォルダー：

*監視により、クラスター XXX の「エクスポート」ストレージがおよそ「85%」いっぱいであることが検出されました。*
*必要に応じて、使用状況を確認したり、クリーンアップを実行したり、アップサイズをリクエストしたりします。*
*また、ストレージが重大しきい値レベルに達すると、アップサイズが自動的に試行されることに注意してください。*

## 原因：

メールはを参照しています **エクスポート** ストレージ。ファイル/メディアに割り当てられているディスクの容量で、という名前の特定のフォルダではありません。 *エクスポート*.

## 解決策

環境でのファイルの使用状況を確認する必要があります。 次のコマンドを実行して、既存の使用方法を取得します。

`df -h |grep data`

ファイルストレージが一杯になる一般的な場所は、次のとおりです。 *pub/media/catalog/product/cache* または *var/log* フォルダー。 ファイルが使用しているディスク領域を調べるには、適切なパスを指定してこのコマンドを実行します */path/to/folder*:

`du -shc` */path/to/folder*

メディア・ディスクの使用量がディスク領域全体の大部分を占める場合は、有効にすることを検討してください [Fastly Deep Image Optimization](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization#deep-image-optimization)に保存されているファイルを削除します *pub/media/catalog/product/cache* サーバー上のフォルダーを手動で設定します。

## 関連資料

[専用クラスターの確認](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space#check-dedicated-clusters) サポートナレッジベースで。