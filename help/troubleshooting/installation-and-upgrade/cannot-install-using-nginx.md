---
title: nginx を使用してインストールできません
description: この記事では、nginx web サーバを使用する際にAdobe Commerceのインストールに失敗した場合の修正方法を説明します。
exl-id: 0af90c7e-0733-41c8-b217-9595b133fa95
feature: Install, Upgrade
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# nginx を使用してインストールできません

この記事では、nginx web サーバを使用する際にAdobe Commerceのインストールに失敗した場合の修正方法を説明します。

## 問題

nginx web サーバを使用している場合にAdobe Commerce ソフトウェアをインストールしようとすると、インストールが失敗することがあります。

## 解決策

`var/report` ディレクトリで次のエラーが発生すると、この問題を確認できます。

```php
NOTE: You cannot install Adobe Commerce using the Setup Wizard because the Adobe Commerce setup directory cannot be accessed.
You can install Adobe Commerce using either the command line or you must restore access to the following directory: /var/www/html/setup
If you are using the sample nginx configuration, please go to http://ce.mtf03.bcn.magento.com/setup/";i:1;s:641:"#0 /var/www/html/lib/internal/Magento/Framework/App/Http.php(213): Magento\Framework\App\Http->redirectToSetup(Object(Magento\Framework\App\Bootstrap), Object(Exception))
```

### 回避策

[ コマンドライン ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced) を使用してAdobe Commerce ソフトウェアをインストールします。
