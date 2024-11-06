---
title: 'Adobe Commerce オンプレミス 2.4.2:product image missing'
description: ここでは、Adobe Commerce オンプレミス 2.4.2 で商品イメージが商品ページにアップロードされない既知の問題について説明します。 この問題は、バージョン 2.4.3 以降のバージョンで対処される予定です。現時点では利用できる解決策はありませんが、回避策として、Nginx を無効にして画像のサイズを変更できます。
exl-id: c4d9240e-5df5-4eab-bb4e-1f06f9bd3a1e
feature: Iaas, Products, Storefront
role: Admin
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Adobe Commerce オンプレミス 2.4.2：製品イメージがありません

ここでは、Adobe Commerce オンプレミス 2.4.2 で商品イメージが商品ページにアップロードされない既知の問題について説明します。 この問題は、バージョン 2.4.3 以降のバージョンで対処される予定です。現時点では利用できる解決策はありませんが、回避策として、Nginx を無効にして画像のサイズを変更できます。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.2

## 問題

製品画像は `s3` バケットに保存されますが、`pub/media` ディレクトリには同期されません。 この問題は、次の両方を使用した場合にのみ発生します。

* サイト対応 Nginx による画像のサイズ変更
* AWS `s3` as media storage

<u> 前提条件 </u>:

Adobe Commerceは Nginx と共にインストールされます。

<u> 再現手順 </u>:

1. AWS `s3` をメディアストレージとして使用するようにAdobe Commerceを設定します。
1. Adobe Commerce インストールディレクトリに用意されている `nginx.conf.sample` 設定ファイルと Nginx バーチャルホストを使用して、Nginx を設定します。 開発者向けドキュメントの [Nginx の設定 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/web-server/nginx) を参照してください。
1. 1 つの製品画像でシンプルな製品を作成します。
1. Nginx には、次のような `nginx.conf.sample` で画像のサイズ変更を行うコメントなしの設定があります。

```conf
load_module /etc/nginx/modules/ngx_http_image_filter_module.so;
location /media/ {
    location ~* ^/media/catalog/.* {
        set $width "-";
        set $height "-";
        if ($arg_width != '') {
            set $width $arg_width;
        }
        if ($arg_height != '') {
            set $height $arg_height;
        }
        image_filter resize $width $height;
        image_filter_jpeg_quality 90;
    }
```

<u> 期待される結果 </u>:

製品画像が製品ページにアップロードされます。

<u> 実際の結果 </u>:

製品画像は製品ページにアップロードされません。

## 回避策

Nginx を無効にして画像のサイズを変更します。
