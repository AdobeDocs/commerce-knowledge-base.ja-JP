---
title: MySQL テーブルが大きすぎます
description: この記事では、MySQL テーブルが 1 GB を超える場合に問題になる理由と、これを防ぐ方法について説明します。
exl-id: 43f74e3b-7f2e-428c-9964-56d2ce98a34d
feature: Services
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# MySQL テーブルが大きすぎます

この記事では、MySQL テーブルが 1 GB を超える場合に問題になる理由と、これを防ぐ方法について説明します。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー 2.x.x 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.x.x

## 問題

MySQL テーブルのサイズは、サイトのパフォーマンスに直接影響しません。 ただし、テーブルが大きい場合は、このテーブルに対する挿入操作が頻繁に行われ、余分なデータや古いデータが含まれている可能性があります。 MySQL は、読み取り/書き込み操作の比率が 80%/20% のデータベース向けに設計されています。  大きなテーブルの場合、1 GB 以上の場合、読み取り操作のパフォーマンスを高速化するように設計された MySQL インデックスは、書き込み操作のパフォーマンスを低下させる可能性があります。

## 解決策

パフォーマンスの低下を避けるために、次のオプションを考慮してください。

* 大きなテーブルをクリーンアップする CRON ジョブを作成します。 大きなテーブルを特定する方法に関する推奨事項については、サポートナレッジベースの [ 大きな MySQL テーブルの検索 ](/help/how-to/general/find-large-mysql-tables.md) を参照してください。
* 1 GB を超えるテーブルの場合は、ログ書き込み用に最適化された MySQL エンジンを使用します。 例えば、アーカイブエンジンなどです。
* ログを DB に保存しないように機能を更新します。

## 関連資料

[ 変更ログテーブルのサイズが大きすぎて、エンティティの更新に遅延が発生する ](/help/troubleshooting/database/changes-in-the-database-are-not-reflected-on-the-storefront.md)、アドビのサポートナレッジベースに記載されています。
