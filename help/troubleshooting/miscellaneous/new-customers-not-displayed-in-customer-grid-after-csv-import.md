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

この記事では、`.csv` ファイルから読み込んだ後、**顧客**/**すべての顧客** の下に新しい顧客が表示されない問題を修正します。 解決策は、`customer_grid` インデクサーを「保存時に更新」モードに設定し、手動でカスタマーグリッドを再インデックス化することです。

## 影響を受けるバージョン

* Adobe Commerce オンプレミス 2.2.0 以降
* クラウドインフラストラクチャー 2.2.0 以降でのAdobe Commerce

## 問題

Adobe Commerceのネイティブ読み込み機能を使用して、`.csv` ファイルから新しい顧客を読み込んだ後、`customer_grid` インデクサーを手動で再インデックス化するまで、管理者の **顧客**/**すべての顧客** に新しい顧客レコードが表示されない場合があります。

## 原因：

Adobe Commerce 2.2.0 以降の「スケジュールに従って更新」インデックス作成モードでは、パフォーマンスの問題が原因で `customer_grid` インデクサーをサポートしていません。

## 解決策

「保存時に更新」モードを使用して、インデックスを再作成する `customer_grid` インデクサーを設定します。 これを行うには、次の手順を実行します。

1. Commerce Admin にログインします。
1. **システム**/**ツール**/**インデックス管理** をクリックします。
1. 「カスタマーグリッドインデクサー」の横にあるチェックボックスをオンにします。
1. **アクション** ドロップダウンリストで、「*保存時に更新*」を選択します。
1. **送信** をクリックします。

また、インデックス作成モードを設定した後は、インデックスが最新で cron で動作するように、`customer_grid` インデクサーのインデックスを手動で再作成することをお勧めします。 手動でインデックスを再作成するには、次のコマンドを使用します。

`bin/magento indexer:reindex customer_grid`

## 詳細情報

開発者向けドキュメントの関連トピックへのリンク：

* [ インデックス作成の概要 ](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/indexing.html)
* [ インデクサーの管理 ](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-index.html)
