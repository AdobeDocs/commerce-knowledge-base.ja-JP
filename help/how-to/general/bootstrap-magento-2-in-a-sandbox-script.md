---
title: サンドボックススクリプトのBootstrap Adobe Commerce 2
description: サンプルサンドボックススクリプトでAdobe Commerce 2 アプリケーションを初期化するには、Adobe Commerce ルートディレクトリから次のスクリプトを実行します。
exl-id: a6acb30a-5175-42c6-8de3-e80c9ae8dac1
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%
---
# サンドボックススクリプトのBootstrap Adobe Commerce 2

サンプルサンドボックススクリプトでAdobe Commerce 2 アプリケーションを初期化するには、Adobe Commerce ルートディレクトリから次のスクリプトを実行します。

```php
<?php

error_reporting(E_ALL | E_STRICT);
ini_set('display_errors', 1);

require __DIR__ . '/app/bootstrap.php';
$bootstrap = \Magento\Framework\App\Bootstrap::create(BP, $_SERVER);
$objectManager = $bootstrap->getObjectManager();

//$model = $objectManager->get('Vendor\Module\Some\Model');
```
