---
title: Adobe Commerce Redis の問題を修正するための最新のパッチをインストールします。
description: この記事では、[Adobe Commerce on cloud infrastructure Patches] （https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches）パッケージで利用可能な最新の Redis 関連パッチについて説明します。
exl-id: 0335bc11-f679-4629-b4e7-6a0e68c3ae44
feature: Cache, Install, Services
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Adobe Commerce Redis の問題を修正するための最新のパッチをインストールします。

Adobe Commerceこの記事では、[&#x200B; クラウドインフラストラクチャー上のパッチ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches) パッケージで利用可能な最新の Redis 関連パッチについて説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.3.3、2.3.4

## 問題

Redis による追加の CPU とメモリ消費は、Adobe Commerceのパフォーマンスを低下させ、Web サイトの全体的なパフォーマンスを低下させる可能性があります。

## 解決策

Adobe Commerce on cloud infrastructure のパッチパッケージから提供される最新のパッチを適用します。 手順について詳しくは、開発者向けドキュメントの [&#x200B; パッチの適用 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches) を参照してください。

Adobe Commerce on cloud infrastructure Patches パッケージが提供する最新の Redis パッチは、次の影響を及ぼします。

* redis のネットワーク通信のサイズを縮小する
* 余分なメモリ消費につながる競合状態の修正
* エビクション・ケースに対応するキャッシュ・アダプタの変更
* redis CPU 消費の削減

Adobe Commerceは、クラウドインフラストラクチャー 2.3.3 以降でAdobe Commerceを実行している場合は、Redis 5 にアップグレードすることをお勧めします。
