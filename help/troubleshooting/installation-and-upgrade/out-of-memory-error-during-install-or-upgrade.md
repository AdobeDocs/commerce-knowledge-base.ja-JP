---
title: インストールまたはアップグレード中のメモリ不足エラー
description: この記事では、Adobe Commerce オンプレミス製品およびMagento Open Sourceオンプレミス製品のインストール/アップグレード中のメモリ不足エラーのソリューションについて説明します。
exl-id: c0ed8228-9357-4a3b-a102-1119386ea52a
feature: Install, Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

アドビの開発者向けドキュメントでは、インストールまたはアップグレードが正常に完了するように [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings)2 GB のメモリを PHP に割り当てる  を推奨しています。

既に設定されている場合は、スワップファイルをマシン上に作成します。 Linux マシンは、より多くのメモリリソースが必要で、RAM がいっぱいであれば *スワップ領域* を使用します。 スワップ領域は、メモリ内の非アクティブなページに使用されます。

次に示すのは、提案のみです。その他のオプションも利用できる場合があります。 続行する前に、ネットワーク管理者またはその他の知識のあるリソースに問い合わせてください。 スワップファイルを `root` 権限を持つユーザーとして作成するには、これらのコマンドを実行する必要があります。

### Ubuntu でファイルをスワップ {#swap-file-on-ubuntu}

以下の参照で説明されているように、`fallocate` コマンドを使用します。

* [Ubuntu 14.04 でスワップを追加する方法（Digitalocean） ](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04)
* [Ubuntu 16.04 でスワップ領域を追加する方法（Digitalocean） ](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04)
* [SwapFaq （help.ubuntu.com） ](https://help.ubuntu.com/community/SwapFaq)

### CentOS でファイルをスワップ {#swap-file-on-centos}

以下の参照で説明されているように、`mkswap` コマンドを使用します。

* [CentOS 6 でスワップを追加する方法（Digitalocean） ](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-6)
* [CentOS 7 でスワップを追加する方法（Digitalocean） ](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-7)
* [ スワップ領域（RedHat カスタマーポータル） ](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-swapspace.html)
