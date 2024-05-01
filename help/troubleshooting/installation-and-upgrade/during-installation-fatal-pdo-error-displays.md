---
title: インストール中に、致命的な PDO エラーが表示される
description: この記事では、インストール中に発生した例外の致命的な PDO エラーを修正します。
exl-id: d69908f0-71c9-48de-9369-6ada22f2b393
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# インストール中に、致命的な PDO エラーが表示される

この記事では、インストール中に発生した例外の致命的な PDO エラーを修正します。

## 問題

```php
PHP Fatal error:  Class 'PDO' not found in /var/www/html/magento2/setup/module/Magento/Setup/src/Module/Setup/ConnectionFactory.php on line 44
```

## 解決策

必ずすべての [必要な PHP 拡張モジュール](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/php-settings.html).
