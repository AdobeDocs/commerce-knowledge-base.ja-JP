---
title: インストール時に PHP の日付を警告
description: この記事では、インストール時の PHP の日付警告を修正します。
exl-id: f82c77a9-bbcd-4426-96a0-b3f4b704860b
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---

# インストール時に PHP の日付を警告

この記事では、インストール時の PHP の日付警告を修正します。

## 詳細 {#details}

インストール中に、次のメッセージが表示されます。

```text
PHP Warning:  date(): It is not safe to rely on the system's timezone settings. [more]
```

### 解決策 {#solution}

PHP のタイムゾーンの設定は慎重に確認してください。 こちらを参照してください [インストールガイド > PHP 設定](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html) 開発者向けドキュメントを参照してください。
