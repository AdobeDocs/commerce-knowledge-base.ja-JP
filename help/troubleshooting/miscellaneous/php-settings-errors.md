---
title: PHP 設定エラー
description: この記事では、PHP の設定エラーに対する解決策を提供します。
exl-id: 51fb3c95-2e25-4d86-a6cf-e08e90d097ca
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# PHP 設定エラー

この記事では、PHP の設定エラーに対する解決策を提供します。

## PHP メモリ制限エラー

準備チェックにより、PHP プロセス用に少なくとも 1GB のメモリが確保されます。 この設定は、オプションのサンプルデータのインストールを含む、ほとんどのインストールで十分です。 ただし、デバッグには少なくとも 2 GB をお勧めします。

PHP のメモリ制限を増やすには、次の手順に従います。

1. Adobe Commerce サーバーにログインします。
1. 次のコマンドを使用して、`php.ini` ファイルを見つけます。

   ```
   bash    $ php --ini
   ```

1. `root` 権限を持つユーザーは、テキストエディターを使用して、`Loaded Configuration File` で指定した `php.ini` を開きます。
1. `memory_limit` を見つけます。
1. 通常の使用とデバッグの場合は、値を `2GB` に変更します。
1. `php.ini` への変更を保存し、テキストエディターを終了します。
1. Web サーバーを再起動します。 次に例を示します。

   * CentOS: `service httpd restart`
   * Ubuntu: `service apache2 restart`
   * nginx （CentOS と Ubuntu の両方）:`service nginx restart`

1. もう一度インストールを試してください。

## 大きなフォームによる max-input-vars エラー

レビュー、製品、属性、オプションの数が多い設定では、設定された PHP の制限を超えるフォームが生成される場合があります。 送信された値の数が `php.ini` 内に設定された `max-input-vars` 限値を超えた場合（デフォルトは 1000）、残りのデータは転送されず、これらのデータベースの値は更新されません。 この場合、PHP ログに次の警告が表示されます。

```bash
PHP message: PHP Warning: Unknown: Input variables exceeded 1000. To increase the limit change max_input_vars in php.ini.
```

`max-input-vars` には「適切な」値はありません。設定のサイズと複雑さによって異なります。 必要に応じて、`php.ini` ファイルの値を変更します。 [ 必要な PHP 設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings) を参照してください。

## xdebug 最大関数のネスト レベル エラー

[ インストール中、xdebug の最大関数のネスト レベル エラー ](/help/troubleshooting/miscellaneous/installation-xdebug-maximum-function-nesting-level-error.md) を参照してください。

## PHTML テンプレートにアクセスすると、エラーが表示されます

通常、エラーテキストは次のようになります。

```bash
Parse error: syntax error, unexpected 'data' (T_STRING)
```

### 解決策：php.ini で `asp_tags = off` を設定します

複数のテンプレートには、製品画像を表示するための次の [ テンプレート ](https://github.com/magento/magento2/blob/2.0/app/code/Magento/Catalog/view/adminhtml/templates/product/edit/base_image.phtml) のように、タグでラップされたテンプレートの抽象レベルをサポートする構文があります（Twig のよ `<% %>` に様々なテンプレートエンジンを使用します）。

```php
<img
    class="product-image"
    src="<%- data.url %>"
    data-position="<%- data.position %>"
    alt="<%- data.label %>" />
```

[asp\_tags](http://php.net/manual/en/ini.core.php#ini.asp-tags) の詳細情報。

`php.ini` を編集して `asp_tags = off` を設定します。 詳しくは、[PHP の設定が必要 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/php-settings) を参照してください。
