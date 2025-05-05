---
title: 暗号化キーに関する問題の解決
description: この記事では、暗号化キーが DB ダンプと一緒に他の環境に移動されないことによって発生する問題を修正する方法について説明します。
exl-id: 34410da0-1bd5-421e-9cd7-d3ee75ad8ed7
feature: Cache, Variables
role: Developer
source-git-commit: 0458b37e2af4c9ad2ec92a1fdd6844ef222ef84a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 暗号化キーに関する問題の解決

この記事では、暗号化キーが DB ダンプと一緒に他の環境に移動されないことによって発生する問題を修正する方法について説明します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.x 上のAdobe Commerce

## 問題

実稼動環境からステージング環境または統合環境に [ データベースダンプ ](/help/how-to/general/create-database-dump-on-cloud.md) を読み込むと、保存されたクレジットカード番号が間違って表示されるか、マーチャント資格情報の使用が必要な支払い統合で支払いが失敗します。

## 原因：

クレジットカード番号や加盟店資格情報などの機密データの暗号化に使用される暗号化キーは、データベースには格納されないので、データベースダンプのインポート/エクスポート後に他の環境に転送されません。

## 解決策

ソース環境から暗号化キーをコピーし、宛先環境に追加する必要があります。

暗号化キーをコピーするには：

1. 開発者向けドキュメントの [ 環境への SSH](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/secure-connections.html?lang=ja) に記載されているように、データベースダンプのソースとなったプロジェクトに SSH で接続します。
1. `app/etc/env.php` をテキストエディターで開きます。
1. `crypt` の `key` の値をコピーします。

```php
return array ('crypt' =>      array ('key' => '<your encryption key>', ),);
```

宛先プロジェクトのキー値を設定するには：

1. [Cloud Console](https://console.adobecommerce.com) を開き、プロジェクトを探します。
1. 開発者向けドキュメントの [ プロジェクトの設定 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=ja) の説明に従って、（開発者向けドキュメントの [CRYPT\_KEY](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html?lang=ja) 変数の値を設定します。 これにより、デプロイメントプロセスがトリガーさ `CRYPT_KEY`、デプロイメントのたびに `app/etc/env.php` ファイルで上書きされます。

オプションで、`app/etc/env.php` ファイルの暗号化キーを手動で上書きできます。

1. 宛先環境に SSH で接続します。
1. `app/etc/env.php` をテキストエディターで開きます。
1. コピーしたデータを `crypt` の `key` 値として貼り付けます。
1. 編集した `env.php` を保存します。
1. `bin/magento cache:clean` を実行するか、Commerce管理の **システム**/**ツール**/**キャッシュ管理** で、宛先環境のキャッシュをクリーンアップします。
