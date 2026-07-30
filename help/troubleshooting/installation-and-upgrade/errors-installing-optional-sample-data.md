---
title: オプションのサンプルデータのインストール中にエラーが発生する
description: このトピックでは、オプションのサンプルデータのインストールで発生する可能性のあるエラーの解決策について説明します。
exl-id: 14692e3a-188c-45f1-9df5-ac873cc9eff0
feature: Console, Install, Upgrade
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# オプションのサンプルデータのインストール中にエラーが発生する

このトピックでは、オプションのサンプルデータのインストールで発生する可能性のあるエラーの解決策について説明します。

## 症状（ファイルシステムの権限）

セットアップウィザードを使用したサンプルデータのインストール中にコンソールログにエラーが発生する：

```php
Module 'Magento_CatalogRuleSampleData':
[ERROR] exception 'Magento\Framework\Exception\LocalizedException' with message 'Can't create directory /var/www/html/magento2/generated/code/Magento/CatalogRule/Model/.' in /var/www/html/magento2/lib/internal/Magento/Framework/Code/Generator.php:103

(more)

Next exception 'ReflectionException' with message 'Class Magento\CatalogRule\Model\RuleFactory does not exist' in /var/www/html/magento2/lib/internal/Magento/Framework/Code/Reader/ClassReader.php:29

(more)
```

これらの例外は、ファイルシステムの権限設定に起因します。

### Solution

[&#x200B; ファイルシステムの所有権と権限を`root`権限を持つユーザーとして再度設定](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/file-system-permissions.html)します。

## 症状（実稼動モード）

現在[実稼動モード &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html)に設定されている場合、[magento sampledata:deploy](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/sample-data/composer-packages.html) コマンドを使用すると、サンプルデータのインストールが失敗します。

```php
PHP Fatal error: Uncaught TypeError: Argument 1 passed to Symfony\Component\Console\Input\ArrayInput::__construct() must be of the type array, object given, called in /<path>/vendor/magento/framework/ObjectManager/Factory/AbstractFactory.php on line 97 and defined in /<path>/vendor/symfony/console/Symfony/Component/Console/Input/ArrayInput.php:37
```

### Solution

サンプルデータは実稼動モードにインストールしないでください。 開発者モードに切り替えて、一部の`var` ディレクトリをクリアし、もう一度試してください。

次のコマンドを、[Adobe Commerce ファイルシステム オーナー](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/overview.html)の順に入力します。

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

### Solution

サンプルデータのインストール時に、次のようなリソースを使用してSELinuxを無効にします。

* [www.ibm.com](https://www.ibm.com/docs/ja/ahts/4.0?topic=t-disabling-selinux)
* [CentOS ドキュメント](https://docs.centos.org/en-US/docs/)

## 症状（分岐の開発）

その他のエラーは次のように表示されます。

```php
[Magento\Setup\SampleDataException] Error during sample data installation: Class Magento\Sales\Model\Service\OrderFactory does not exist
```

### Solution

Adobe Commerce開発ブランチでサンプルデータを使用する際に、既知の問題があります。 代わりにmaster ブランチを使用してください。 次のようにマスターブランチに切り替えることができます。

```php
cd <magento_root>
git checkout master
git pull origin master
```

## 症状（max_execution_time）

サンプルデータのインストールが完了する前に、インストールが停止します。 例は次のとおりです。

```php
(more)

Module 'Magento_CustomerSampleData':
Installing data...
```

サンプルデータのインストールが完了しません。

このエラーは、PHP スクリプトの最大設定実行時間を超えた場合に発生します。 サンプルデータの読み込みに時間がかかる場合があるので、インストール時に値を増やすことができます。

### Solution

`root`権限を持つユーザーは、`php.ini`を変更して、`max_execution_time`の値を600以上に増やします。 （600分は10分。 値を任意に増やすことができます）。 インストールが成功したら、`max_execution_time`を以前の値に戻す必要があります。

`php.ini`の場所がわからない場合は、次のコマンドを入力します。

```php
php --ini
```

`Loaded Configuration File`の値は、変更する必要がある`php.ini`です。

>[!NOTE]
>
>私たちは、この記事には、一部の人が人種差別的、性差別的、または抑圧的であると感じる可能性があり、読者が傷つけられ、トラウマを負わされ、または歓迎されないと感じる可能性がある、業界標準のソフトウェア用語がまだ含まれている可能性があることを認識しています。 Adobeでは、コード、ドキュメント、ユーザーエクスペリエンスからこれらの用語を削除しようと取り組んでいます。
