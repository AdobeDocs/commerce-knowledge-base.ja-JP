---
title: CSV の読み込み後、新しい顧客がカスタマーグリッドに表示されない
description: この記事では、「.csv」ファイルから読み込んだ後、**Customers** &gt; **All customers**の下に新しい顧客が表示されない問題を修正します。 解決策は、「customer_grid」インデクサーを「保存時に更新」モードに設定し、手動でカスタマーグリッドを再インデックス化することです。
exl-id: e4d9d60a-a0d1-4602-924e-a338e56de61d
feature: Data Import/Export
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# CSV の読み込み後、新しい顧客がカスタマーグリッドに表示されない

この記事では、の下に新しい顧客が表示されない問題の修正について説明します **顧客** > **すべての顧客** からインポートした後 `.csv` ファイル。 解決策は、 `customer_grid` 「保存時に更新」モードへのインデクサーを行い、カスタマーグリッドを手動でインデックス再作成します。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス 2.2.0 以降
* クラウドインフラストラクチャー 2.2.0 以降でのAdobe Commerce

## 問題

から新規顧客を読み込んだ後 `.csv` ネイティブのAdobe Commerce読み込み機能を使用しているファイルでは、以下に新しい顧客レコードを表示できない場合があります **顧客** > **すべての顧客** 管理者でを手動で再インデックス化するまで `customer_grid` インデクサー。

## 原因：

Adobe Commerce 2.2.0 以降の「スケジュールに従って更新」インデックス作成モードでは、 `customer_grid` パフォーマンスの問題が原因でインデクサーが使用されました。

## 解決策

の設定 `customer_grid` 「保存時に更新」モードを使用してインデックスを再作成するインデクサー。 これを行うには、次の手順を実行します。

1. Commerce Admin にログインします。
1. クリック **システム** > **ツール** > **インデックス管理**.
1. 「カスタマーグリッドインデクサー」の横にあるチェックボックスをオンにします。
1. が含まれる **アクション** ドロップダウンリストから「」を選択します *保存時の更新*.
1. クリック **Submit**.

また、を手動でインデックス再作成することをお勧めします `customer_grid` インデックスモードの設定後、インデックスが最新であり、cron で動作することを確認するためにインデクサーを行います。 手動でインデックスを再作成するには、次のコマンドを使用します。

`bin/magento indexer:reindex customer_grid`

## 詳細情報

開発者向けドキュメントの関連トピックへのリンク：

* [インデックス作成の概要](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/indexing.html)
* [インデクサーの管理](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-index.html)
