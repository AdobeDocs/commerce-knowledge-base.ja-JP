---
title: PHP設定エラー
description: この記事では、PHP設定エラーの解決策を提供します。
exl-id: 51fb3c95-2e25-4d86-a6cf-e08e90d097ca
feature: Configuration
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%
---
# PHP設定エラー

この記事では、PHP設定エラーの解決策を提供します。

## PHP メモリ制限エラー

準備状況チェックでは、PHP プロセス用に少なくとも1 GBのメモリが確保されていることを確認します。 この設定は、オプションのサンプルデータのインストールなど、ほとんどのインストールで十分です。 ただし、デバッグには少なくとも2 GBを推奨します。

PHPのメモリ制限を増やすには：

1. Adobe Commerce サーバーにログインします。
1. 次のコマンドを使用して、`php.ini` ファイルを探します。

   ```
   bash    $ php --ini
   ```

1. `root`権限を持つユーザーは、テキストエディターを使用して、`Loaded Configuration File`で指定された`php.ini`を開きます。
1. `memory_limit`を探します。
1. 通常の使用とデバッグでは、値`2GB`に変更します。
1. 変更を`php.ini`に保存して、テキストエディターを終了します。
1. Web サーバーを再起動します。 次に例を示します。

   * CentOS: `service httpd restart`
   * Ubuntu: `service apache2 restart`
   * nginx （CentOSとUbuntuの両方）: `service nginx restart`

1. インストールを再試行してください。

## フォームが大きいため、max-input-vars エラーが発生する

ストアビュー、製品、属性、またはオプションの数が多い設定では、事前に設定したPHPの制限を超えるフォームを生成できます。 送信された値の数が`php.ini`内で設定された`max-input-vars`制限を超えた場合（デフォルトは1000）、残りのデータは転送されず、それらのデータベース値は更新されません。 この場合、警告がPHP ログに表示されます。

```bash
PHP message: PHP Warning: Unknown: Input variables exceeded 1000. To increase the limit change max_input_vars in php.ini.
```

`max-input-vars`には「適切な」値がありません。設定のサイズと複雑さによって異なります。 必要に応じて、`php.ini` ファイルの値を変更します。 [必要なPHP設定](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/php-settings)を参照してください。

## xdebug最大関数のネスト レベル エラー

[ インストール中に、xdebug最大関数のネスト レベル エラー](/help/troubleshooting/miscellaneous/installation-xdebug-maximum-function-nesting-level-error.md)を参照してください。

## PHTML テンプレートにアクセスするとエラーが表示される

通常、エラーテキストは次のとおりです。

```bash
Parse error: syntax error, unexpected 'data' (T_STRING)
```

### 解決策：php.iniで`asp_tags = off`を設定

複数のテンプレートには、テンプレートの抽象レベルをサポートするための構文があります（Twigなどの異なるテンプレートエンジンを使用します）。製品イメージを表示するには、次の[ テンプレート ](https://github.com/magento/magento2/blob/2.0/app/code/Magento/Catalog/view/adminhtml/templates/product/edit/base_image.phtml)のように、`<% %>` タグで囲まれます。

```php
<img
    class="product-image"
    src="<%- data.url %>"
    data-position="<%- data.position %>"
    alt="<%- data.label %>" />
```

[asp\_tags](http://php.net/manual/en/ini.core.php#ini.asp-tags)の詳細情報。

`php.ini`を編集して`asp_tags = off`を設定します。 詳しくは、[必要なPHP設定](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/php-settings)を参照してください。
