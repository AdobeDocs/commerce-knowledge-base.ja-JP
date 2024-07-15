---
title: オプションのサンプルデータのインストール中にエラーが発生しました
description: このトピックでは、オプションのサンプル データのインストールで発生する可能性のあるエラーの解決策について説明します。
exl-id: 14692e3a-188c-45f1-9df5-ac873cc9eff0
feature: Console, Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# オプションのサンプルデータのインストール中にエラーが発生しました

このトピックでは、オプションのサンプル データのインストールで発生する可能性のあるエラーの解決策について説明します。

## 現象（ファイル・システムの権限）

セットアップウィザードを使用したサンプルデータのインストール中にコンソールログにエラーが表示される：

```php
Module 'Magento_CatalogRuleSampleData':
[ERROR] exception 'Magento\Framework\Exception\LocalizedException' with message 'Can't create directory /var/www/html/magento2/generated/code/Magento/CatalogRule/Model/.' in /var/www/html/magento2/lib/internal/Magento/Framework/Code/Generator.php:103

(more)

Next exception 'ReflectionException' with message 'Class Magento\CatalogRule\Model\RuleFactory does not exist' in /var/www/html/magento2/lib/internal/Magento/Framework/Code/Reader/ClassReader.php:29

(more)
```

これらの例外は、ファイルシステムの権限設定から発生します。

### 解決策

[ ファイルシステムの所有権と権限を、`root` 権限を持つユーザーとして ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/file-system-permissions.html) 再度設定します。

## 症状（実稼動モード）

現在 [ 実稼動モード ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html) に設定している場合、[magento sampledata:deploy](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/sample-data/composer-packages.html) コマンドを使用すると、サンプルデータのインストールが失敗します。

```php
PHP Fatal error: Uncaught TypeError: Argument 1 passed to Symfony\Component\Console\Input\ArrayInput::__construct() must be of the type array, object given, called in /<path>/vendor/magento/framework/ObjectManager/Factory/AbstractFactory.php on line 97 and defined in /<path>/vendor/symfony/console/Symfony/Component/Console/Input/ArrayInput.php:37
```

### 解決策

実稼動モードでサンプルデータをインストールしないでください。 開発者モードに切り替え、`var` のディレクトリの一部をクリアして、もう一度試してください。

次のコマンドを、[Adobe Commerce ファイルシステムの所有者 ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/overview.html) として表示されている順序で入力します。

```php
cd <magento_root>
bin/magento deploy:mode:set developer
rm -rf generated/code/* generated/metadata/*
bin/magento sampledata:deploy
```

## 症状（セキュリティ）

オプションのサンプルデータをインストールすると、次のようなメッセージが表示されます。

```php
PHP Fatal error: Call to undefined method Magento\Catalog\Model\Resource\Product\Interceptor::getWriteConnection() in /var/www/magento2/app/code/Magento/SampleData/Module/Catalog/Setup/Product/Gallery.php on line 144
```

### 解決策

サンプルデータのインストール中に、次のようなリソースを使用して SELinux を無効にします。

* [www.ibm.com](https://www.ibm.com/docs/ja/ahts/4.0?topic=t-disabling-selinux)
* [CentOS のドキュメント ](https://docs.centos.org/en-US/docs/)

## 症状（発達分枝）

その他に、次のようなエラーが表示されます。

```php
[Magento\Setup\SampleDataException] Error during sample data installation: Class Magento\Sales\Model\Service\OrderFactory does not exist
```

### 解決策

Adobe Commerce開発ブランチでサンプルデータを使用する場合、既知の問題があります。 代わりに、マスターブランチを使用します。 マスターブランチに切り替えるには、次の手順を実行します。

```php
cd <magento_root>
git checkout master
git pull origin master
```

## 症状（max_execution_time）

インストールは、サンプルのデータのインストールが完了する前に停止します。 次に例を示します。

```php
(more)

Module 'Magento_CustomerSampleData':
Installing data...
```

サンプルデータのインストールが完了しない。

このエラーは、設定されている PHP スクリプトの実行時間が上限を超えた場合に発生します。 サンプルデータの読み込みには長い時間がかかることがあるので、インストール中に値を増やすことができます。

### 解決策

`root` 権限を持つユーザーとして、`php.ini` を変更して `max_execution_time` の値を 600 以上に増やします。 （600 秒は 10 分 値は任意に増やすことができます）。 インストールが正常 `max_execution_time` 完了したら、を以前の値に戻す必要があります。

`php.ini` の場所がわからない場合は、次のコマンドを入力します。

```php
php --ini
```

`Loaded Configuration File` の値は、変更する必要がある `php.ini` です。

>[!NOTE]
>
>この記事には、人種差別的、性差別的、または抑圧的と思われる業界標準のソフトウェア用語が依然として含まれており、読者が苦痛を感じたり、トラウマを抱いたり、歓迎されないと感じたりする場合があることを認識しています。 Adobeでは、これらの用語をアドビのコード、ドキュメントおよびユーザーエクスペリエンスから削除するよう取り組んでいます。
