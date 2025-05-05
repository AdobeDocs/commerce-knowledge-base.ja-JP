---
title: インストール中に、致命的な PDO エラーが表示される
description: この記事では、インストール中に発生した例外の致命的な PDO エラーを修正します。
exl-id: d69908f0-71c9-48de-9369-6ada22f2b393
feature: Install, Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
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

必ず [ 必要な PHP 拡張機能 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings) をすべてインストールしてください。
