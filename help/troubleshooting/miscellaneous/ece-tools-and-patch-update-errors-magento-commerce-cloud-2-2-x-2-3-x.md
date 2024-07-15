---
title: ECE ツールとパッチアップデートエラーAdobe Commerce Cloud Infrastructure 2.2.x.、2.3.x
description: この記事では、ECE ツール、パッチ、またはその他の変更に対して更新をデプロイしようとすると、「*ストリームを開けませんでした：*」や「*そのようなファイルやディレクトリがありません*」などのエラーメッセージが表示される問題の解決策を説明します。
exl-id: b1658001-0ffd-4f8a-a15f-d785efcee51f
feature: Cloud, Paas
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# ECE ツールとパッチアップデートエラーAdobe Commerce Cloud Infrastructure 2.2.x.、2.3.x

この記事では、ECE-Tools、パッチ、またはその他の変更に対して更新をデプロイしようとすると、「*ストリームを開けませんでした：*」や「*そのようなファイルやディレクトリがありません*」などのエラーメッセージが表示される問題の解決策を説明します。

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー上のAdobe Commerce 2.2.x.、2.3.x

## 問題

ECE-Tools、パッチ、その他の変更をデプロイしようとするとエラーが発生します。Cloud Console と `var/log/cloud.log` の PHP エラー

```
W: PHP Warning: require(<path to file>): failed to open stream: No such file or directory in <path to file> on line 70
W: PHP Fatal error: require(): Failed opening required '<path to file>;'
(include_path='<path to file>') in <path to file> on line 70

Warning: require(/app/vendor/composer/../../app/etc/NonComposerComponentRegistration.php):
failed to open stream: No such file or directory in /app/vendor/composer/autoload_real.php
on line 70

Fatal error: require(): Failed opening required '/app/vendor/composer/../../app/etc/NonComposerComponentRegistration.php'
(include_path='/app/vendor/magento/zendframework1/library:.:/usr/share/php')
in /app/vendor/composer/autoload_real.php on line 70

E: Error building project: Step failed with status code 255.
```

例外ログエラー：

```
CRITICAL:
error: <path to missing file>: No such file or directory
```

```
W: Generating optimized autoload files
W: PHP Warning: Uncaught ErrorException: require(<path to file>):
failed to open stream: No such file or directory in <path to file>
```

```
PHP Warning: Uncaught Exception: Warning: require(/app/setup/config/application.config.php):
failed to open stream: No such file or directory in /app/vendor/magento/framework/Console/Cli.php
on line 63 in /app/vendor/magento/framework/App/ErrorHandler.php:61
```

```
[Symfony\Component\Console\Exception\CommandNotFoundException]
 W: There are no commands defined in the "module" namespace.
```

## 原因：

`composer.json` ファイルの設定ミス。

## 解決策

`composer.json` ファイルに設定がない場合、一部のディレクトリはAdobe Commerce コードベースからコピーされません。 ファイルが見つからないため、パッケージと更新/修正プログラムを適用できません。

以下に示す内容に合わせて追加のセクションを変更し、デプロイメントを再試行してください。

```
"extra":{
  "magento-force": true,
  "magento-deploystrategy": "copy"
}
```

## 関連資料

* 開発者向けドキュメントの [ アップグレードとパッチ ](https://devdocs.magento.com/guides/v2.3/cloud/project/project-upgrade-parent.html?itm_source=devdocs&amp;itm_medium=search_page&amp;itm_campaign=federated_search&amp;itm_term=update%20ece%20tools)。
