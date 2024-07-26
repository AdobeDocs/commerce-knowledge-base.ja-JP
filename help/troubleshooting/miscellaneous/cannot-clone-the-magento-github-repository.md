---
title: Magento GitHub リポジトリを複製できません
description: この記事では、Magento GitHub リポジトリを複製できない場合の解決策を説明します。
exl-id: 65de77b5-496d-42a3-ab2e-1fff9df97160
feature: Data Import/Export
role: Developer
source-git-commit: 35d4f2130d0ec71f71f5f20aa8a7c76207e7a35a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# Magento GitHub リポジトリを複製できません

この記事では、Magento GitHub リポジトリを複製できない場合の解決策を説明します。

## 詳細 {#detail}

次のようなエラーが発生します。

```bash
Cloning into 'magento2'...
Permission denied (publickey).
fatal: The remote end hung up unexpectedly
```

## 解決策 {#solution}

[GitHub ヘルプページ ](https://help.github.com/articles/generating-ssh-keys) の説明に従って、SSH キーを GitHub にアップロードします。
