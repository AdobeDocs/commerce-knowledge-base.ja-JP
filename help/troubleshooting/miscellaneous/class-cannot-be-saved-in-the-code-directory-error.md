---
title: 「コードディレクトリにクラスを保存できません」エラー」
description: この記事では、依存関係を指定した方法によりクラスがその場で自動生成されなくなり、「Class cannot be saved in the generated/code directory」*というエラーメッセージが表示される問題の修正方法を説明します。
exl-id: e2c00d4d-31c3-4446-a317-a8ac92c707d5
feature: Configuration
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 「クラスをコードディレクトリに保存できません」エラー

この記事では、依存関係を指定した方法により、クラスがその場で自動生成されなくなる問題を修正する方法を説明します。その結果、 *「生成された/コードディレクトリにクラスを保存できません」* エラーメッセージ。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.2.0 以降でのAdobe Commerce

## 問題

<u>再現手順</u>

1. ローカル環境で、自動生成されたクラスに依存するカスタムクラスを作成します。
1. カスタムクラスがトリガーされるシナリオを実行し、正しく機能していることを確認します。
1. 変更をコミットして統合環境にプッシュします。 これにより、デプロイメントプロセスがトリガーになります。 デプロイメントに成功しました。
1. が含まれる [統合環境](/help/announcements/adobe-commerce-announcements/integration-environment-enhancement-request-pro-and-starter.md)、カスタムクラスがトリガーされるシナリオを実行します。

<u>期待される結果</u>

ローカル環境と同様に、すべてが正しく機能します。

<u>実際の結果</u>

クラスをに保存できないというエラーメッセージで失敗 `generated/code` ディレクトリ。

## 原因：

この問題の原因は、依存関係が存在するクラスは、デプロイメント中に生成されず、クラスがトリガーされたときに後で生成することができないためです `generated/code` 配置が完了した後、ディレクトリを書き込めません。

この問題が発生する主な理由は次の 2 つです。

* ケース 1：自動生成されたクラスに依存するクラスは、エントリポイント（ `index.php` ）に設定します。これは、デプロイメント時に依存関係のスキャンを行いません。
* ケース 2：自動生成クラスへの依存関係が直接指定されている（依存関係を宣言するためのコンストラクターの推奨使用方法と比較）。

## 解決策

どちらの場合にも共通する解決策の 1 つは、自動生成されたクラスではなく、実際のファクトリを作成することです。

または、ケースごとに特定の解決策があります。

### 事例 1 固有の解決策

クラス コードをエントリ ポイントから別のモジュールに移動し、エントリ ポイントで使用します。

<u>例</u>

内の元のコード（例：） `index2.php` :

```php
<?php
use YourVendor\SomeModule\Model\GeneratedFactory;

require realpath(__DIR__) . '/../app/bootstrap.php';
$bootstrap = \Magento\Framework\App\Bootstrap::create(BP, $_SERVER);

class SomeClass
{
    private $generatedFactory;

    public function __construct(GeneratedFactory $generatedFactory)
    {
        $this->generatedFactory = $generatedFactory;
    }

// Some code here...
}

$someObject = $bootstrap->getObjectManager()->create(SomeClass::class);

// There is some code that uses $someObject
```

次の手順を実行する必要があります。

1. クラス定義をに移動します `app/code/YourVendor/YourModule`:

   ```php
      <?php
       namespace YourVendor\YourModule;
       use YourVendor\YourModule\Model\GeneratedFactory;
       class YourClass
       {
           private $generatedFactory;
   
           public function __construct(GeneratedFactory $generatedFactory)
           {
               $this->generatedFactory = $generatedFactory;
           }
       // Some code here...
       }
   ```

1. エントリポイントを編集 `my_api/index.php` 次のように表示されます。

   ```php
     <?php
     use YourVendor\YourModule\YourClass;
         require realpath(__DIR__) . '/../app/bootstrap.php';
         $bootstrap = \Magento\Framework\App\Bootstrap::create(BP, $_SERVER);
         $someObject = $bootstrap->getObjectManager()->create(YourClass::class);
     // Some code using $someObject
   ```

### 事例 2）特有の解決策

依存関係の宣言をコンストラクターに移動します。

<u>例</u>

元のクラス宣言：

```php
<?php
namespace YourVendor\YourModule;

use YourVendor\SomeModule\Model\GeneratedFactory;
use Magento\Framework\App\ObjectManager;

class YourClass
{
    private $generatedFactory;
    private $someParam;

    public function __construct($someParam)
    {
        $this--->someParam = $someParam;
        $this->generatedFactory = ObjectManager::getInstance()->get(GeneratedFactory::class);
    }

    // Some code here...
}
```

コンストラクタは、次のように変更する必要があります。

```php
<?php
namespace YourVendor\YourModule;

use YourVendor\YourModule\Model\GeneratedFactory;
use Magento\Framework\App\ObjectManager;

class YourClass
{
    private $generatedFactory;
    private $someParam;

    public function __construct($someParam, GeneratedFactory $generatedFactory = null)
    {
        $this->someParam = $someParam;
        $this->generatedFactory = $generatedFactory ?: ObjectManager::getInstance()->get(GeneratedFactory::class);
    }

    // Some code here...
}
```

## 関連資料

* [コードの生成](https://devdocs.magento.com/guides/v2.3/extension-dev-guide/code-generation.html) 開発者向けドキュメントを参照してください。
