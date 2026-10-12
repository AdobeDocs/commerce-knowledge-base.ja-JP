---
title: Adobe Commerce cloud：再インデックスは「Killed」メッセージで終了します
description: '* Adobe Commerce on cloud インフラストラクチャ（すべてのバージョン）'
exl-id: 36ed9c9f-8280-41db-9df3-fe842dade4b1
feature: Cloud, Paas
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%
---
# Adobe Commerce cloud：再インデックスは`Killed` メッセージで終了します

## 影響を受ける製品とバージョン

* Adobe Commerce on cloud infrastructure （すべてのバージョン）

## イシュー

統合ブランチ （またはスターターアーキテクチャプロジェクトのステージング）でインデックス再作成を実行しようとしています。プロセスは`Killed` メッセージで終了しています。

## 原因

これは通常、PHP プロセスのメモリ不足が原因で発生します。
その最も一般的な理由は、インスタンス上の多数の製品、ストア、顧客グループです。

## Solution

1. 製品数を減らします（該当する場合は、顧客グループと店舗だけでなく）。
1. 同時ユーザーを1人または2人に制限します。
1. cron ジョブを無効にし、必要に応じて手動で実行します。
1. 以前に行われていない場合は、拡張統合環境へのアップグレードをリクエストします。アップグレードが実行されると制限される環境数の制限に注意してください。 詳しくは、サポートナレッジベースの「[統合環境の機能強化リクエスト - ProおよびStarter](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27242)」の記事を参照してください。

## 関連トピックス：

アドビの開発者ドキュメントには、次のようなものがあります。

* [プロアーキテクチャ/統合環境](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/pro-architecture#integration-environment)
* [スターターアーキテクチャ > ステージング環境](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/architecture/starter-architecture#cloud-arch-stage)
