---
title: 「Adobe Commerce cloud：再インデックスが「強制終了」メッセージで終了します」
description: '* クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）'
exl-id: 36ed9c9f-8280-41db-9df3-fe842dade4b1
feature: Cloud, Paas
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Adobe Commerce cloud：再インデックスは `Killed` メッセージで終了します

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce（すべてのバージョン）

## 問題

統合ブランチ（またはスターターアーキテクチャプロジェクトのステージング）で再インデックスを実行しようとしていますが、`Killed` のメッセージでプロセスが終了しています。

## 原因：

これは通常、PHP のプロセスがメモリ不足になっているために起こります。
これが生じる最も一般的な理由は、インスタンス上に多数の製品、ストア、顧客グループが存在することです。

## 解決策

1. 製品の数を減らします（該当する場合は、顧客グループおよび店舗も減らします）。
1. 使用を 1 人または 2 人の同時ユーザーに制限します。
1. cron ジョブを無効にし、必要に応じて手動で実行します。
1. これを行ったことがない場合は、Enhanced Integration 環境へのアップグレードをリクエストします。アップグレードが実行されると制限される環境の数の制限に注意してください。 詳しくは、サポートナレッジベースの [ 統合環境強化リクエスト - Pro と Starter](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md) の記事を参照してください。

## 関連資料：

開発者向けドキュメントでは、

* [Pro アーキテクチャ > 統合環境 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment)
* [ スターターアーキテクチャ/ステージング環境 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#cloud-arch-stage)
