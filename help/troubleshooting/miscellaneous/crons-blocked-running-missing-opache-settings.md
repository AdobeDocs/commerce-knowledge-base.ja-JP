---
title: Cron が設定の誤りや欠落によって停止する [!DNL OpCache] 設定
description: この記事では、設定の誤りや欠落が原因で cron の動作が停止した場合の解決策を示します [!DNL OpCache] 設定。
exl-id: 30643ea9-969f-41c8-8e62-b24e56d690cf
feature: Cache
role: Developer
source-git-commit: e223c2e1063b25399cc29a087623435b414e19a6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Cron が設定の誤りや欠落により停止した [!DNL OpCache] 設定

この記事では、Cron が設定の欠落や誤りが原因で動作を停止した場合の解決策を示します [!DNL OpCache] 設定。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce [すべてのサポートされているバージョン](https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf).

## 問題

cron が動作しなくなった。

## 原因：

この [!DNL OpCache] モジュールは、を導入した新しいバージョンに更新されました [!DNL GraphQL] を書き換えるプラグイン `env.php` 実行時に、が cron 設定をオーバーライドする可能性があるので、が問題の原因である可能性があります。 この [!DNL OpCache] の問題を回避するには、設定を更新する必要があります `env.php file`、およびで解決されました [バージョン 2002.1.13](/docs/commerce-cloud-service/user-guide/release-notes/ece-tools-package.html?lang=en#v2002.1.13) の [!DNL ECE Tools] パッケージ。

## 解決策

オプション 1：コマンドラインツールで次を実行します。

```bash
bin/magento cron:run
```

Cron が無効であることを示すメッセージが表示される場合があります。

オプション 2：を開く `app/etc/env.php` ファイル – 以下に示す場合は、cron が手動で無効になっているか、デプロイメントに失敗したために再度有効になっていないか、に関連して問題が発生しています [!DNL OpCache] 設定。

```php
  'cron' =>
  array (
    'enabled' => 0,
  ),
```

1. Cron が無効になっている場合は、次のコマンドを実行して cron を再度有効にします。 `vendor/bin/ece-tools cron:enable`
1. の最新バージョンであることを確認してください [!DNL ECE Tools]. そうでない場合は、をアップグレード（または項目 3 にスキップ）します。 既存のバージョンを確認するには、次のコマンドを実行します。
   `composer show magento/ece-tools`
1. 既にの最新バージョンを使用している場合 [!DNL ECE Tools]、が存在するかどうかを確認します `op-exclude.txt` ファイル。 それには、次のコマンドを実行します。
   `ls op-exclude.txt`.
このファイルが存在しない場合は、https://github.com/magento/magento-cloud/blob/master/op-exclude.txtをリポジトリに追加してから、変更をコミットして再デプロイします。
1. アップグレードする必要がありません [!DNL ECE Tools]また、リポジトリでhttps://github.com/magento/magento-cloud/blob/master/op-exclude.txtを追加または変更したあと、変更をコミットして再デプロイすることもできます。

## 関連資料

* [Cron 準備チェックの問題](/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues.html)
* [Crons プロパティ](/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html)
* [Cron ジョブが「実行中」ステータスでスタックする](/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-job-is-stuck-in-running-status.html)
