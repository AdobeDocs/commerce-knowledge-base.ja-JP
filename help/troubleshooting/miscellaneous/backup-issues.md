---
title: バックアップの問題
description: この記事では、バックアップ作成の問題に対して考えられる解決策を示します。
exl-id: 1a6204ad-bd5a-46dc-8a8e-39655a174e09
feature: Storage, Data Import/Export
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# バックアップの問題

この記事では、バックアップ作成の問題に対して考えられる解決策を示します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.x
* Magento Open Source 2.3.x

## バックアップが無効 {#backup-disabled}

Adobe Commerce バックアップ機能が起動しない場合や、次のメッセージが表示される場合は、バックアップの前に機能を有効にする必要があります。

```terminal
Backup functionality is disabled.
Backup functionality is currently disabled. Please use other means for backups.
```

次の CLI コマンドを入力します。

```bash
bin/magento config:set system/backup/functionality_enabled 1
```

バックアップの詳細については、を参照してください [ファイル・システム、メディア、データベースをバックアップおよびロール・バックします。](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli-backup.html)

## ディスク容量が不足しています {#insufficient-disk-space-trouble-backup-space-}

ディスク領域が不十分なためにバックアップが失敗した場合は、通常、一部のファイルを別のストレージデバイスまたはドライブに移動して、ディスク領域を解放する必要があります。 ただし、この問題を解決する他の方法がある場合があります。 ヒントについては、次のリソースのいずれかを参照してください。

* [Linux および Unix システムのハードディスクの問題（ディスク容量超過やディスクへの書き込み不可など）を解決するための 8 つのヒント](https://www.cyberciti.biz/datacenter/linux-unix-bsd-osx-cannot-write-to-hard-disk)
* [serverfault: df はディスクがいっぱいと言うが、ディスクが空ではない](https://serverfault.com/questions/315181/df-says-disk-is-full-but-it-is-not)
* [unix.stackexchange.com:Linux のディスク容量がどこにあるかを調べますか？](https://unix.stackexchange.com/questions/125429/tracking-down-where-disk-space-has-gone-on-linux)

## オペレーティングシステムエラー {#operating-system-error-trouble-backup-os-}

残念ながら、発生する可能性のある様々なエラーにより、具体的なものはお勧めできません。 ただし、次のことをお勧めします。

* システム管理者にお問い合わせください。
* 次のような公開フォーラムを検索 [スタック交換](https://unix.stackexchange.com) または [スタック オーバーフロー](https://stackoverflow.com)
* を開く [GitHub の問題](https://github.com/magento/magento2/issues) そして、我々は助けるためにしようとします。

## バックアップの失敗 {#backup-fails-trouble-backup-all-}

バックアップが失敗した場合、またはすべてのバックアップテストが失敗した場合、 [Adobe Commerce ファイルシステムの所有者](https://devdocs.magento.com/guides/v2.2/install-gde/prereq/file-sys-perms-over.html) には、Adobe Commerce ファイルシステムの十分な権限と所有権がありません。 例えば、別のユーザーがファイルを所有している場合や、ファイルが読み取り専用の場合などです。

ファイルシステムの権限と所有者に特に注意してください `<magento_root>/var` ディレクトリとサブディレクトリ。 詳しくは、を参照してください [ファイルシステムの権限と所有権の設定](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/file-system-perms.html).
