---
title: 無効なオフセットエラーを解決します
description: ここでは、Adobe Commerce 2.1 以降で、Commerce Admin
exl-id: 62d16d3c-7f4b-45e9-ae4b-fe2b58cc3620
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 無効なオフセットエラーを解決します

ここでは、Adobe Commerce 2.1 以降で、Commerce Admin

Adobe Commerce 2.1 以降では、Commerce Admin で新しい商品を作成すると、次のエラーが表示される場合があります。

```text
Warning: Illegal string offset 'is_in_stock' in [...]/vendor/
magento/module-catalog-inventory/Ui/DataProvider/Product/Form/
Modifier/AdvancedInventory.php on line 87
```

## 詳細

Adobe Commerce 2.1 以降では、`Magento\Framework\Api\ExtensionAttributesFactory.php` の [`getExtensionAttributes`](https://github.com/magento/magento2/blob/2.3/lib/internal/Magento/Framework/Api/ExtensionAttributesFactory.php#L64-L73) メソッドの `getDocComment` 検証呼び出しで PHP コードコメントを使用します。

PHP OPcache （推奨）を有効にした場合、デフォルトでは OPcache 設定 [`opcache.save_comments`](http://php.net/manual/en/opcache.configuration.php#ini.opcache.save_comments) が無効になっているため、このエラーが表示されます。

## 回避策

この問題を解決するには、OPcache 設定を探し、次のように有効 `opcache.save_comments` します。

### 手順 1:OPcache 設定を見つける

#### OPcache 構成設定を検索する手順は、次のとおりです。

PHP OPcache の設定は、通常 `php.ini` または `opcache.ini` に置かれます。 場所は、オペレーティングシステムと PHP のバージョンによって異なる場合があります。 OPcache 構成ファイルには、`[opcache]` セクションまたは `opcache.enable` のような設定が含まれる場合があります。

検索には、次のガイドラインを使用します。

* Apache web サーバー：<br>

Apache を使用する Ubuntu の場合、OPcache 設定は通常 `php.ini` にあります。<br>
Apache または nginx を使用する CentOS の場合、OPcache 設定は通常 `/etc/php.d/opcache.ini` にあります。<br>
存在しない場合は、次のコマンドを使用して検索します。

```bash
    $ sudo find / -name 'opcache.ini'
```

* php-FPM を使用する nginx web サーバ：`/etc/php5/fpm/php.ini`。

複数の `opcache.ini` がある場合は、それらをすべて変更します。


### 手順 2:`opcache.save_comments` を有効にする

1. OPcache 構成ファイルをテキスト・エディタで開きます。
1. `opcache.save_comments` を見つけ、必要に応じてコメントを解除します。
1. その値が `1` に設定されていることを確認します。
1. 変更を保存し、テキストエディターを終了します。
1. Web サーバーを再起動します。

   * Apache、Ubuntu:`service apache2 restart`
   * Apache、CentOS: `service httpd restart`
   * nginx、Ubuntu、CentOS: `service nginx restart`

1. DI 構成および自動生成できる不足しているクラスをすべて再生成します：

```bash
    $ bin/magento setup:di:compile`
```
