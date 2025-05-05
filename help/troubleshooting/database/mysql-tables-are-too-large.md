---
title: '[!DNL MySQL] テーブルが大きすぎます'
description: この記事では、任意のテーブルが 1 GB を超えると問題が発生する理由と  [!DNL MySQL]  れを防ぐ方法について説明します。
exl-id: 43f74e3b-7f2e-428c-9964-56d2ce98a34d
feature: Services
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# [!DNL MySQL] テーブルが大きすぎます

この記事では、[!DNL MySQL] テーブルが 1 GB を超えると問題が発生する理由と、それを防ぐ方法について説明します。

## 影響を受ける製品とバージョン：

* クラウドインフラストラクチャー 2.x.x 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.x.x

## 問題

[!DNL MySQL] のテーブルサイズは、サイトのパフォーマンスに直接影響しません。 ただし、テーブルが大きい場合は、このテーブルに対する挿入操作が頻繁に行われ、余分なデータや古いデータが含まれている可能性があります。 [!DNL MySQL] は、読み取り/書き込みオペレーションの比率が 80%/20% であるデータベース向けに設計されています。  大きなテーブルの場合、読み取り操作のパフォーマンスを高速化するように設計された [!DNL MySQL] インデックスを 1 GB 以上にすると、書き込み操作のパフォーマンスが低下する可能性があります。

## 解決策

パフォーマンスの低下を避けるために、次のオプションを考慮してください。

* 大きなテーブルをクリーンアップする CRON ジョブを作成します。 大きなテーブルを特定する方法に関する推奨事項については、サポートナレッジベースの [ 大きなテーブルの検索 ](/help/how-to/general/find-large-mysql-tables.md) を参照してください  [!DNL MySQL] 
* テーブルが 1 GB を超える場合は、ログ書き込み用に最適化された [!DNL MySQL] エンジンを使用します。 例えば、アーカイブエンジンなどです。
* ログを DB に保存しないように機能を更新します。

## 関連資料

* [ 変更ログテーブルのサイズが大きすぎて、エンティティの更新に遅延が発生する ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/database/changes-in-the-database-are-not-reflected-on-the-storefront) アドビのサポートナレッジベース
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
