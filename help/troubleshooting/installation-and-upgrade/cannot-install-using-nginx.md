---
title: nginx を使用してインストールできません
description: この記事では、nginx web サーバを使用する際にAdobe Commerceのインストールに失敗した場合の修正方法を説明します。
exl-id: 0af90c7e-0733-41c8-b217-9595b133fa95
feature: Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# nginx を使用してインストールできません

この記事では、nginx web サーバを使用する際にAdobe Commerceのインストールに失敗した場合の修正方法を説明します。

## 問題

nginx web サーバを使用している場合にAdobe Commerce ソフトウェアをインストールしようとすると、インストールが失敗することがあります。

## 解決策

この問題は、次のエラーで確認できます `var/report` ディレクトリ：

```php
NOTE: You cannot install Adobe Commerce using the Setup Wizard because the Adobe Commerce setup directory cannot be accessed.
You can install Adobe Commerce using either the command line or you must restore access to the following directory: /var/www/html/setup
If you are using the sample nginx configuration, please go to http://ce.mtf03.bcn.magento.com/setup/";i:1;s:641:"#0 /var/www/html/lib/internal/Magento/Framework/App/Http.php(213): Magento\Framework\App\Http->redirectToSetup(Object(Magento\Framework\App\Bootstrap), Object(Exception))
```

### 回避策

を使用してAdobe Commerce ソフトウェアをインストールします。 [コマンドライン](https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli.html).
