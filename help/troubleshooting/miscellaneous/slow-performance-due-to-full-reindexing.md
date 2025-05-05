---
title: インデックス再作成が完全なのでパフォーマンスが低下する
description: この記事では、完全なインデックス再作成（インデックス作成関連のデータベーステーブル内のデータが更新中の場合）によるパフォーマンス低下の修正について説明します。
exl-id: 4f20a862-cf54-4196-8a88-101f0c80f8f1
feature: Best Practices
role: Developer
source-git-commit: 72ee49a8667f575a58e0cf1b3d5c9df936cc628b
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# インデックス再作成が完全なのでパフォーマンスが低下する

この記事では、完全なインデックス再作成（インデックス作成関連のデータベーステーブル内のデータが更新中の場合）によるパフォーマンス低下の修正について説明します。

## 影響を受けるバージョンと製品

* クラウドインフラストラクチャー 2.x.x 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.x.x

### 問題

継続的なフラッシュやインデックスの再構築は、パフォーマンスが低下する理由の一部です。 さらに、完全なインデックス再作成を継続的に行うと、テーブルにロックが追加され、web サイトの動作が予想よりはるかに遅くなります。

### 原因：

完全なインデックス再作成を実行できるアクションは、管理者から実行されました。例えば、次のようなものがあります。

* 製品属性の保存
* Web サイト/ストア/ストアビューの保存
* ストアの設定

>[!NOTE]
>
>これらのアクションを営業時間外に実行して、営業時間内のパフォーマンスに影響を与えないようにする必要があります。

[ サードパーティの拡張機能 ](https://support.magento.com/hc/en-us/articles/360042361152-Best-Practices-for-using-third-party-extensions-in-Magento) によって、完全なインデックス再作成が行われることもあります。 完全な再インデックスは、CLI から手動で実行することもできます。 インデックスが再作成され、パフォーマンスが低下する可能性があるかどうかを確認するには、次の手順を実行します。

1. 次のクエリを実行して、過去 15 分間に完全に再インデックスされたインデクサーを検索します。

   ```
   SELECT * FROM indexer_state WHERE updated > NOW() - INTERVAL 15 MINUTE;
   ```

   出力内のインデクサー名は、インデクサーが過去 15 分間に少なくとも 1 回はインデックスを再作成されたことを意味します。

1. 完全なインデックス再作成を頻繁に行っていた場合は、次の点を調査してください。
   * CLI から手動で実行する可能性のあるユーザー
   * インデックス再作成を行っているサードパーティモジュール
   * インデクサーを「無効 *とマークするサードパーティモジュール*

### 解決策

必要な場合にのみ、インデックス再作成を実行します。 手順については、開発者向けドキュメントの [ インデクサーの設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers) を確認してください。 一般的な推奨事項とベストプラクティスは、部分的なインデックス再作成メカニズムによって、マーチャントによる手動アクションを必要とせずに、データのインデックス再作成を処理できるようにすることです。 すべてのインデックス再作成は、Adobe Commerceのネイティブ機能（Mview）を使用して行う必要があります。 Mview は、データのインデックスを再作成する最も効率的な方法である部分インデックス再作成を実行します。 Mview について詳しくは、開発者向けドキュメントの [ インデックス作成の概要：Mview](https://developer.adobe.com/commerce/php/development/components/indexing/#mview) を参照してください。

## 関連資料

* [ インデックス作成の概要：インデックス再作成方法 ](https://developer.adobe.com/commerce/php/development/components/indexing/#how-to-reindex) については、開発者向けドキュメントを参照してください。
* [ 無効化されたキャッシュは、サポートナレッジベースで応答時間の低下を引き起こします ](/help/troubleshooting/miscellaneous/invalidated-cache-causes-response-time-degradation.md)。

