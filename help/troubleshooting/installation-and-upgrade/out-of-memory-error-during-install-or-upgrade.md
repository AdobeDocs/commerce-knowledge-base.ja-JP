---
title: インストールまたはアップグレード中のメモリ不足エラー
description: この記事では、Adobe Commerce オンプレミス製品およびMagento Open Sourceオンプレミス製品のインストール/アップグレード中のメモリ不足エラーのソリューションについて説明します。
exl-id: c0ed8228-9357-4a3b-a102-1119386ea52a
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# インストールまたはアップグレード中のメモリ不足エラー

この記事では、Adobe Commerce オンプレミス製品およびMagento Open Sourceオンプレミス製品のインストール/アップグレード中のメモリ不足エラーのソリューションについて説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.x
* オンプレミス 2.3.x のMagento Open Source

## 問題

Web セットアップウィザードを使用して、Adobe CommerceまたはMagento Open Sourceアプリケーション、または拡張機能、テーマ、言語パッケージなどのコンポーネントをインストールまたはアップデートすると、次のようなエラーが表示されます。

```bash
Could not complete update {"components":[
{"name":"magento/module-bundle-sample-data","version":"100.1.0"}
]} successfully: proc_open(): fork failed - Cannot allocate memory
```

エラー

```bash
proc_open(): fork failed - Cannot allocate memory
```

はコマンドラインにも表示できます。

## 解決策 {#solution}

お勧めです [2GB のメモリを PHP に割り当てる](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html) 開発者向けドキュメントで、インストールまたはアップグレードが正常に完了したことを確認します。

既に設定されている場合は、スワップファイルをマシン上に作成します。 Linux マシンでは、を使用します *スワップ領域* より多くのメモリリソースが必要で、RAM がいっぱいである場合。 スワップ領域は、メモリ内の非アクティブなページに使用されます。

次に示すのは、提案のみです。その他のオプションも利用できる場合があります。 続行する前に、ネットワーク管理者またはその他の知識のあるリソースに問い合わせてください。 スワップファイルをユーザーとして作成するには、次のコマンドを実行する必要があります。 `root` 権限。

### Ubuntu でファイルをスワップ {#swap-file-on-ubuntu}

の使用 `fallocate` 以下の参照で説明されているコマンド。

* [Ubuntu 14.04 でスワップを追加する方法（Digitalocean）](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04)
* [Ubuntu 16.04 でスワップ領域を追加する方法（Digitalocean）](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04)
* [SwapFaq （help.ubuntu.com）](https://help.ubuntu.com/community/SwapFaq)

### CentOS でファイルをスワップ {#swap-file-on-centos}

の使用 `mkswap` 以下の参照で説明されているコマンド。

* [CentOS 6 でスワップを追加する方法（Digitalocean）](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-6)
* [CentOS 7 でスワップを追加する方法（Digitalocean）](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-7)
* [スワップ領域（RedHat カスタマーポータル）](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-swapspace.html)
