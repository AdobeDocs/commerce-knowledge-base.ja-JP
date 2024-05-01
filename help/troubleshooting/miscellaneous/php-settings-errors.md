---
title: PHP 設定エラー
description: この記事では、PHP の設定エラーに対する解決策を提供します。
exl-id: 51fb3c95-2e25-4d86-a6cf-e08e90d097ca
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
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
1. を見つけます。 `php.ini` 次のコマンドを使用してファイルを送信します。

   ```
   bash    $ php --ini
   ```

1. を使用した As a ユーザー `root` 権限がある場合、テキストエディターを使用してを開く `php.ini` 指定者 `Loaded Configuration File`.
1. を見つける `memory_limit`.
1. 値に変更します `2GB` （通常の使用およびデバッグ用）。
1. 変更をに保存します。 `php.ini` をクリックして、テキストエディターを終了します。
1. Web サーバーを再起動します。 次に例を示します。

   * CentOS: `service httpd restart`
   * Ubuntu: `service apache2 restart`
   * nginx （CentOS と Ubuntu の両方）: `service nginx restart`

1. もう一度インストールを試してください。

## 大きなフォームによる max-input-vars エラー

レビュー、製品、属性、オプションの数が多い設定では、設定された PHP の制限を超えるフォームが生成される場合があります。 送信された値の数がを超えた場合 `max-input-vars` 内に設定された制限 `php.ini` （デフォルトは 1000）。残りのデータは転送されず、これらのデータベース値は更新されません。 この場合、PHP ログに次の警告が表示されます。

```terminal
PHP message: PHP Warning: Unknown: Input variables exceeded 1000. To increase the limit change max_input_vars in php.ini.
```

に「適切」な値がありません `max-input-vars`設定のサイズと複雑さに応じて異なります。 の値を変更します `php.ini` 必要に応じて、ファイルを作成します。 参照： [必要な PHP 設定](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html).

## xdebug 最大関数のネスト レベル エラー

参照： [インストール中に、xdebug の最大関数のネスト レベル エラーが発生する](/help/troubleshooting/miscellaneous/installation-xdebug-maximum-function-nesting-level-error.md).

## PHTML テンプレートにアクセスすると、エラーが表示されます

通常、エラーテキストは次のようになります。

```terminal
Parse error: syntax error, unexpected 'data' (T_STRING)
```

### 解決策：設定 `asp_tags = off` php.ini

複数のテンプレートには、でラップされたテンプレート（Twig のような異なるテンプレートエンジンを使用）に抽象レベルをサポートする構文があります。 `<% %>` タグ、例：次のタグ [template](https://github.com/magento/magento2/blob/2.0/app/code/Magento/Catalog/view/adminhtml/templates/product/edit/base_image.phtml) 商品画像の表示：

```php
<img
    class="product-image"
    src="<%- data.url %>"
    data-position="<%- data.position %>"
    alt="<%- data.label %>" />
```

に関する詳細情報 [asp\_tags](http://php.net/manual/en/ini.core.php#ini.asp-tags).

編集 `php.ini` およびを設定 `asp_tags = off`. 詳しくは、を参照してください [必要な PHP 設定](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html).
