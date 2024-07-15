---
title: インストール中に、リフレクション例外エラーが発生する
description: この記事では、インストール中のリフレクション例外エラーの解決策について説明します。
exl-id: aed5f297-1339-4171-9392-04b3f93277ee
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# インストール中に、リフレクション例外エラーが発生する

この記事では、インストール中のリフレクション例外エラーの解決策について説明します。

## 詳細 {#details}

インストール中に、次のようなメッセージが表示されます。

```php
[ERROR] exception 'ReflectionException' with message 'Class Magento\Framework\StoreManagerInterface does not exist' in /<path>/lib/internal/Magento/Framework/Code/Reader/ClassReader.php
```

## 解決策 {#solution}

Adobe Commerce サブディレクトリの下のすべてのディレクトリとファイル `var` クリアし、Adobe Commerce ソフトウェアを再度インストールします。

[Adobe Commerce ファイルシステムのオーナー ](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/file-sys-perms-over.html) または `root` 権限を持つユーザーとして、次のコマンドを入力します。

```bash
$ cd <your Magento install directory>/var
```

```bash
$ rm -rf var/cache/* di/* generation/* page_cache/*
```

### Redis {#redis}

Redis を使用してもエラーが発生する場合は、次のように Redis キャッシュをクリアします。

```bash
$ redis-cli FLUSHALL
```
