---
title: サポートエージェントから要求された場合に「スクラブ」ダンプを作成する方法
description: この記事では、Adobe Commerce サポートエージェントから提供を依頼された場合に、Adobe Commerce管理者からデータベースの「スクラブ」ダンプ（バックアップ）とコードを作成する方法について説明します。 このダンプは、メディアファイルを除外して、プロセスを高速化し、ファイルを大幅に小さくします。 データベースのバックアップを作成する際に、すべての機密データがハッシュ化されます。
exl-id: ad088bd2-3f92-416e-89f0-d037d53cd6a9
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# サポートエージェントから要求された場合に「スクラブ」ダンプを作成する方法


## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.3.x、2.4.x。

## 「スクラブ」ダンプの作成

管理者から「スクラブ」ダンプを作成します。

1. Commerce Adminで、**System** > **Support** > **Data Collector**&#x200B;に移動します。
1. 「**新規バックアップ**」をクリックします。
1. 数分後、「**ステータスを更新**」をクリックします（完了するまで5分ごとに繰り返す場合があります）。
1. 生成されたダンプファイルを`/var/support` ディレクトリからAdobe Commerce ルートディレクトリに再配置します。

次に、ダンプファイルへの直接ダウンロードリンク（ストアアドレスと表示されているファイル名）をサポートするように指定できます。

管理者からダンプを作成する際に問題が発生した場合は、開発者ドキュメントの[ サポートユーティリティの実行](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/run-support-utilities)で説明されているように、CLI コマンドを使用することを検討してください。

## 関連トピックス

* [ クラウドインフラストラクチャ上のAdobe Commerceのデータベースの完全なバックアップを作成](/help/how-to/general/create-database-dump-on-cloud.md)します。
