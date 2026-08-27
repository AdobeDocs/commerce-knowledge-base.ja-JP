---
title: 無効なオフセットエラーを解決する
description: この記事では、Adobe Commerce 2.1以降で、Commerce Adminで新しい商品を作成する際に「無効なオフセットを解決する」エラーが表示される場合の解決策を紹介します。
exl-id: 62d16d3c-7f4b-45e9-ae4b-fe2b58cc3620
feature: Configuration
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 無効なオフセットエラーを解決する

この記事では、Adobe Commerce 2.1以降で、Commerce Adminで新しい商品を作成する際に「無効なオフセットを解決する」エラーが表示される場合の解決策を紹介します。

Adobe Commerce 2.1以降では、Commerce Adminで新しい商品を作成する際に、次のエラーが表示される場合があります。

```text
Warning: Illegal string offset 'is_in_stock' in [...]/vendor/
magento/module-catalog-inventory/Ui/DataProvider/Product/Form/
Modifier/AdvancedInventory.php on line 87
```

## Details

Adobe Commerce 2.1以降では、`Magento\Framework\Api\ExtensionAttributesFactory.php`の[`getExtensionAttributes`](https://github.com/magento/magento2/blob/2.3/lib/internal/Magento/Framework/Api/ExtensionAttributesFactory.php#L64-L73) メソッドの`getDocComment`検証呼び出しでPHP コードコメントを使用します。

PHP OPcache （推奨）を有効にした場合、OPcache設定[`opcache.save_comments`](http://php.net/manual/en/opcache.configuration.php#ini.opcache.save_comments)はデフォルトで無効になっているため、このエラーが表示されます。

## 回避策

この問題を解決するには、OPcache設定設定を見つけ、次のように`opcache.save_comments`を有効にします。

### 手順1:OPcache設定を探す

#### OPcache構成設定を検索するには、次の手順に従います。

PHP OPcacheの設定は通常、`php.ini`または`opcache.ini`にあります。 場所は、オペレーティングシステムとPHPのバージョンによって異なる場合があります。 OPcache設定ファイルには、`[opcache]` セクションまたは`opcache.enable`のような設定が含まれている場合があります。

次のガイドラインを使用して検索します。

* Apache web サーバー：<br>

Apacheを使用するUbuntuの場合、OPcache設定は通常`php.ini`にあります。<br>
Apacheまたはnginxを使用するCentOSの場合、OPcache設定は通常`/etc/php.d/opcache.ini`にあります。<br>
そうでない場合は、次のコマンドを使用して検索します。

```bash
    $ sudo find / -name 'opcache.ini'
```

* nginx web サーバーとPHP-FPM: `/etc/php5/fpm/php.ini`。

`opcache.ini`が複数ある場合は、それらをすべて変更します。


### 手順2: `opcache.save_comments`を有効にする

1. テキストエディターでOPcache設定ファイルを開きます。
1. `opcache.save_comments`を探し、必要に応じてコメントを解除します。
1. 値が`1`に設定されていることを確認してください。
1. 変更を保存し、テキストエディターを終了します。
1. Web サーバーを再起動します。

   * Apache、Ubuntu: `service apache2 restart`
   * Apache、CentOS: `service httpd restart`
   * nginx、Ubuntu、およびCentOS: `service nginx restart`

1. 自動生成できるDI設定とすべての欠落クラスを再生成します。

```bash
    $ bin/magento setup:di:compile`
```
