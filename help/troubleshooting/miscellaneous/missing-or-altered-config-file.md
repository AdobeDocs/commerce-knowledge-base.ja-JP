---
title: 設定ファイルが見つからないか変更されている
description: Adobe Commerceの設定ファイルが見つからない、または変更されている問題を解決します。
exl-id: d80bf981-8ba6-4357-a841-57bf5d3f2a3f
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 設定ファイルが見つからないか変更されている

この記事では、設定ファイルが変更されたり、失われたりする問題を解決する方法について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべてのバージョン

## 問題

設定ファイル `config.php` や `env.php` が誤って変更されたか、見つかりません。

## 解決策

デプロイメントプロセスでは、設定ファイルごとにバックアップファイルが作成されます。

* `app/etc/config.php.bak` - システム固有の設定を含み、存在しない場合はビルド時に自動生成されます
* `app/etc/env.php.bak` – 機密の構成データを含む

ECE-tools `backup:restore` コマンドを使用して復元できます。

BAK ファイルは、デプロイメントプロセスの産物です。 デプロイ後に手動で設定ファイルを変更した場合、変更内容は既存の BAK ファイルには反映されません。

設定ファイルを復元するには：

1. [SSH](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh) を使用してリモートリポジトリにログインします。
1. 使用可能なバックアップファイルのリストを表示します。

   ```
   ./vendor/bin/ece-tools backup:list
   ```

   ```
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. 設定ファイルを復元します。

   ```
   ./vendor/bin/ece-tools backup:restore
   ```

   復元によって影響を受ける既存の設定ファイルのリストが表示されます。

   ```
   app/etc/env.php file exists! If you want to rewrite existed files use --force
   app/etc/config.php file exists! If you want to rewrite existed files use --force
   ```

1. `--force` オプションを使用して、すべてのファイルを上書きします。

   ```
   ./vendor/bin/ece-tools backup:restore --force
   ```

   ```
   Command backup:restore with option --force will rewrite your existed files. Do you want to continue [y/N]?y
   Backup file app/etc/env.php was restored.
   Backup file app/etc/config.php was restored.
   ```

1. オプションで、特定の設定ファイルを復元できます。

   ```
   ./vendor/bin/ece-tools backup:restore --force --file=app/etc/config.php
   ```

   ```
   Command backup:restore with option --force will rewrite your existed files. Do you want to continue [y/N]?y
   Backup file app/etc/config.php was restored.
   ```
