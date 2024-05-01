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

Adobe Commerce 2.1 以降では、PHP コードのコメントを `getDocComment` での検証呼び出し [`getExtensionAttributes`](https://github.com/magento/magento2/blob/2.3/lib/internal/Magento/Framework/Api/ExtensionAttributesFactory.php#L64-L73) メソッド： `Magento\Framework\Api\ExtensionAttributesFactory.php`.

PHP OPcache （推奨）を有効にした場合、デフォルトでは OPcache 設定が表示されるため、このエラーが表示されます [`opcache.save_comments`](http://php.net/manual/en/opcache.configuration.php#ini.opcache.save_comments) が無効になっています。

## 回避策

この問題を解決するには、OPcache 設定を探し、を有効にします。 `opcache.save_comments` 次のように設定します。

### 手順 1:OPcache 設定を見つける

#### OPcache 構成設定を検索する手順は、次のとおりです。

PHP OPcache の設定は、通常、次の場所にあります。 `php.ini` または `opcache.ini`. 場所は、オペレーティングシステムと PHP のバージョンによって異なる場合があります。 OPcache 構成ファイルには、次のファイルが含まれる場合があります `[opcache]` 次のようなセクションまたは設定 `opcache.enable`.

検索には、次のガイドラインを使用します。

* Apache web サーバー：<br>

Apache を使用する Ubuntu の場合、OPcache 設定は通常、次の場所にあります。 `php.ini`.<br>
Apache または nginx を使用する CentOS の場合、OPcache 設定は通常、にあります。 `/etc/php.d/opcache.ini`.<br>
存在しない場合は、次のコマンドを使用して検索します。

```bash
    $ sudo find / -name 'opcache.ini'
```

* nginx web サーバと PHP-FPM: `/etc/php5/fpm/php.ini`.

2 つ以上の場合 `opcache.ini`を選択し、それらをすべて変更します。


### 手順 2：を有効にする `opcache.save_comments`

1. OPcache 構成ファイルをテキスト・エディタで開きます。
1. を見つける `opcache.save_comments` 必要に応じて、コメントを解除します。
1. その値がに設定されていることを確認します。 `1`.
1. 変更を保存し、テキストエディターを終了します。
1. Web サーバーを再起動します。

   * Apache、Ubuntu: `service apache2 restart`
   * Apache、CentOS: `service httpd restart`
   * nginx、Ubuntu、CentOS: `service nginx restart`

1. DI 構成および自動生成できる不足しているクラスをすべて再生成します：

```bash
    $ bin/magento setup:di:compile`
```
