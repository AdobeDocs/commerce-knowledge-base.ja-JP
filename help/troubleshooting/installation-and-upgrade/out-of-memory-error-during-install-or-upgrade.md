---
title: インストールまたはアップグレード中のメモリ不足エラー
description: この記事では、Adobe Commerce オンプレミスおよびMagento Open Source オンプレミス製品のインストール/アップグレード中に発生するメモリ不足エラーの解決策について説明します。
exl-id: c0ed8228-9357-4a3b-a102-1119386ea52a
feature: Install, Upgrade
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%
---
# インストールまたはアップグレード中のメモリ不足エラー

この記事では、Adobe Commerce オンプレミスおよびMagento Open Source オンプレミス製品のインストール/アップグレード中に発生するメモリ不足エラーの解決策について説明します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.3.x
* Magento Open Source オンプレミス 2.3.x

## イシュー

Web セットアップ ウィザードを使用して、Adobe CommerceまたはMagento Open Source アプリケーションや拡張機能、テーマ、言語パッケージなどのコンポーネントをインストールまたはアップデートすると、次のようなエラーが表示されます。

```bash
Could not complete update {"components":[
{"name":"magento/module-bundle-sample-data","version":"100.1.0"}
]} successfully: proc_open(): fork failed - Cannot allocate memory
```

エラー

```bash
proc_open(): fork failed - Cannot allocate memory
```

コマンド ラインにも表示できます。

## Solution {#solution}

インストールまたはアップグレードが正常に実行されるように、開発者向けドキュメントで2GBのメモリを[PHP](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings)に割り当てることをお勧めします。

既に行っている場合は、マシンにスワップファイルを作成します。 Linux マシンは、メモリ リソースが多く必要でRAMがいっぱいである場合、*スワップ領域*&#x200B;を使用します。 スワップ領域は、メモリ内の非アクティブなページに使用されます。

以下は推奨事項のみです。他のオプションも利用できます。 続行する前に、ネットワーク管理者または他の知識のあるリソースに問い合わせてください。 `root`権限を持つユーザーとしてスワップファイルを作成するには、コマンドを実行する必要があります。

### Ubuntuでのファイルのスワップ {#swap-file-on-ubuntu}

次の参照で説明されているように、`fallocate` コマンドを使用します。

* [Ubuntu 14.04 （Digitalocean）でスワップを追加する方法](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04)
* [Ubuntu 16.04 （Digitalocean）にスワップ領域を追加する方法](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04)
* [SwapFaq （help.ubuntu.com）](https://help.ubuntu.com/community/SwapFaq)

### CentOSでのファイルのスワップ {#swap-file-on-centos}

次の参照で説明されているように、`mkswap` コマンドを使用します。

* [CentOS 6 （Digitalocean）にスワップを追加する方法](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-6)
* [CentOS 7 （Digitalocean）でスワップを追加する方法](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-7)
* [スワップ領域（RedHat カスタマーポータル）](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-swapspace.html)
