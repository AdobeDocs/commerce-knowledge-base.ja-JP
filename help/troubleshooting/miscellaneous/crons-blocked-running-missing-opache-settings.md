---
title: 設定の誤りや設定の欠落が原因で Cron が停止  [!DNL OpCache]  る
description: この記事では、設定の誤りや欠落が原因で cron の動作が停止した場合のソリューショ  [!DNL OpCache]  を示します。
exl-id: 30643ea9-969f-41c8-8e62-b24e56d690cf
feature: Cache
role: Developer
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# [!DNL OpCache] 設定が正しくないか、または見つからないため、Cron が停止しました

この記事では、[!DNL OpCache] 設定が見つからないか設定が誤っているために cron が動作を停止した場合の解決策を示します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce[ サポートされているすべてのバージョン ](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf)。

## 問題

cron が動作しなくなった。

## 原因：

[!DNL OpCache] モジュールは、実行時に `env.php` を書き換える [!DNL GraphQL] プラグインを導入した新しいバージョンに更新され、cron 設定を上書きする可能性があり、問題が発生した可能性があります。 `env.php file` の問題を回避するには [!DNL OpCache] の設定を更新する必要があります。これは、[!DNL ECE Tools] パッケージの [ バージョン 2002.1.13](/docs/commerce-cloud-service/user-guide/release-notes/ece-tools-package.html?lang=en#v2002.1.13) で解決されました。

## 解決策

オプション 1：コマンドラインツールで次を実行します。

```bash
bin/magento cron:run
```

Cron が無効であることを示すメッセージが表示される場合があります。

オプション 2:`app/etc/env.php` ファイルを開く – 以下が表示される場合は、cron が手動で無効になっているか、デプロイメントに失敗したために再度有効になっていないか、問題が [!DNL OpCache] 設定に関連しています。

```php
  'cron' =>
  array (
    'enabled' => 0,
  ),
```

1. cron が無効になっている場合は、次のコマンドを実行して cron を再度有効にします。`vendor/bin/ece-tools cron:enable`
1. 最新バージョンの [!DNL ECE Tools] を使用していることを確認してください。 そうでない場合は、をアップグレード（または項目 3 にスキップ）します。 既存のバージョンを確認するには、次のコマンドを実行します。
   `composer show magento/ece-tools`
1. 既に最新バージョンの [!DNL ECE Tools] を使用している場合は、`op-exclude.txt` ファイルが存在するかどうかを確認します。 それには、次のコマンドを実行します。
   `ls op-exclude.txt`。
このファイルが存在しない場合は、https://github.com/magento/magento-cloud/blob/master/op-exclude.txtをリポジトリに追加してから、変更をコミットして再デプロイします。
1. [!DNL ECE Tools] をアップグレードしなくても、リポジトリでhttps://github.com/magento/magento-cloud/blob/master/op-exclude.txtを追加または変更し、その変更をコミットして再デプロイすることもできます。

## 関連資料

* [Cron 準備チェックの問題](/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues.html)
* [Crons プロパティ](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html)
* [Cron ジョブが「実行中」ステータスでスタックする](/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html)
