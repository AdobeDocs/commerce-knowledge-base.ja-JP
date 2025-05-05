---
title: バックアップの問題
description: この記事では、バックアップ作成の問題に対して考えられる解決策を示します。
exl-id: 1a6204ad-bd5a-46dc-8a8e-39655a174e09
feature: Storage, Data Import/Export
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

```bash
Backup functionality is disabled.
Backup functionality is currently disabled. Please use other means for backups.
```

次の CLI コマンドを入力します。

```bash
bin/magento config:set system/backup/functionality_enabled 1
```

バックアップの詳細については、[ ファイル システム、メディア、およびデータベースのバックアップとロールバック ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/backup) を参照してください。

## ディスク容量が不足しています {#insufficient-disk-space-trouble-backup-space-}

ディスク領域が不十分なためにバックアップが失敗した場合は、通常、一部のファイルを別のストレージデバイスまたはドライブに移動して、ディスク領域を解放する必要があります。 ただし、この問題を解決する他の方法がある場合があります。 ヒントについては、次のリソースのいずれかを参照してください。

* Linux および Unix システムのハードディスクに関する問題（ディスク容量超過やディスクへの書き込み不可など）を解決するための [8 ヒント ](https://www.cyberciti.biz/datacenter/linux-unix-bsd-osx-cannot-write-to-hard-disk)
* [serverfault: df はディスクがいっぱいだと言うが、そうではない ](https://serverfault.com/questions/315181/df-says-disk-is-full-but-it-is-not)
* [unix.stackexchange.com: Linux のディスク領域がどこに移動したかをトラッキングしています。](https://unix.stackexchange.com/questions/125429/tracking-down-where-disk-space-has-gone-on-linux)

## オペレーティングシステムエラー {#operating-system-error-trouble-backup-os-}

残念ながら、発生する可能性のある様々なエラーにより、具体的なものはお勧めできません。 ただし、次のことをお勧めします。

* システム管理者にお問い合わせください。
* [Stack Exchange](https://unix.stackexchange.com) や [Stack Overflow](https://stackoverflow.com) などの公開フォーラムを検索します
* [GitHub イシュー ](https://github.com/magento/magento2/issues) を開くと、お手伝いします。

## バックアップの失敗 {#backup-fails-trouble-backup-all-}

バックアップが失敗した場合、またはすべてのバックアップテストが失敗した場合、[Adobe Commerce ファイルシステムの所有者 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/file-system/overview) に、Adobe Commerce ファイルシステムの十分な権限および所有権がない可能性があります。 例えば、別のユーザーがファイルを所有している場合や、ファイルが読み取り専用の場合などです。

特に、ファイルシステムの権限と、`<magento_root>/var` ディレクトリおよびサブディレクトリの所有権に注意してください。 詳しくは、[ ファイルシステムの権限と所有権の設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions) を参照してください。
