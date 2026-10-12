---
title: インストール中に、Reflection Exception エラーが発生しました
description: この記事では、インストール時のReflection Exception エラーの解決策について説明します。
exl-id: aed5f297-1339-4171-9392-04b3f93277ee
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
source-wordcount: '107'
ht-degree: 0%
---
# インストール中に、Reflection Exception エラーが発生しました

この記事では、インストール時のReflection Exception エラーの解決策について説明します。

## 詳細 {#details}

インストール中に、次のようなメッセージが表示されます。

```php
[ERROR] exception 'ReflectionException' with message 'Class Magento\Framework\StoreManagerInterface does not exist' in /<path>/lib/internal/Magento/Framework/Code/Reader/ClassReader.php
```

## Solution {#solution}

Adobe Commerceの`var` サブディレクトリの下にあるすべてのディレクトリとファイルをクリアし、Adobe Commerce ソフトウェアを再度インストールします。

[Adobe Commerce ファイルシステムの所有者](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/file-system/overview)または`root`権限を持つユーザーとして、次のコマンドを入力します。

```bash
$ cd <your Magento install directory>/var
```

```bash
$ rm -rf var/cache/* di/* generation/* page_cache/*
```

### Redis {#redis}

Redisを使用してもエラーが発生する場合は、次のようにRedis キャッシュをクリアします。

```bash
$ redis-cli FLUSHALL
```
