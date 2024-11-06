---
title: インストール時に PHP の日付を警告
description: この記事では、インストール時の PHP の日付警告を修正します。
exl-id: f82c77a9-bbcd-4426-96a0-b3f4b704860b
feature: Install, Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

PHP のタイムゾーンの設定は慎重に確認してください。 開発者向けドキュメントの [ インストールガイド/PHP 設定 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/php-settings) を参照してください。
