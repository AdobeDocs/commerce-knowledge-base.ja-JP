---
title: ブラウザーでAdobe Commerceにアクセスする際に PHP バージョンエラーまたは 404 エラーが発生する
description: この文書では、Web ブラウザでAdobe Commerce インスタンスにアクセスできず、404 エラーまたは「サポートされていない PHP バージョン」エラーが発生する問題の解決策を示します。
exl-id: 6cfdeaae-5e52-411c-9006-5af8a467873a
feature: Configuration
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# ブラウザーでAdobe Commerceにアクセスする際に PHP バージョンエラーまたは 404 エラーが発生する

この文書では、Web ブラウザでAdobe Commerce インスタンスにアクセスできず、404 エラーまたは「サポートされていない PHP バージョン」エラーが発生する問題の解決策を示します。

## 影響を受ける製品とバージョン：

* Adobe Commerce 2.3.x

## 問題：PHP バージョンがサポートされていません

Adobe Commerce ストアフロントまたはCommerce Admin にアクセスしようとすると、次のメッセージが表示されます。

`Magento supports PHP 7.1.3 or later. Please read Magento System Requirements.`

### 解決策

次の操作を試してください。

* PHP をバージョン 7.3 にアップグレードします。詳しくは、開発者向けドキュメントの [Adobe Commerce 2.3 テクノロジースタックの要件 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/system-requirements) を参照してください。
* Apache を再起動します。ファイルシステムと同じ PHP バージョンを使用していない可能性があるからです。 Apache を再起動するには、次のコマンドを使用します。
   * Ubuntu: `service apache2 restart`
   * CentOS: `service httpd restart`

## 問題：エラー 404

Adobe Commerce ストアフロントまたはCommerce Admin にアクセスしようとすると、404 （見つかりません）エラーが表示されます。

### 解決策

次の操作を試してください。

* [Apache server rewrites](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/web-server/apache) が有効になっていることを確認します。 Apache サーバーの書き換えが正しく設定されていない場合、静的ファイルは正しい場所から提供されません。
* インストール中に入力したベース URL に問題がある可能性があります。 ベース URL の値は、コマンドラインからAdobe Commerceをインストールするときに `--base-url=` を指定するか、web インストーラーの Web 設定ページにある **ストアアドレス** フィールドの値として指定します。 ベース URL *必須* は、スキーム（`http://` など）で始まり、末尾がスラッシュ（/）で終わります。 有効な値でインストーラーを再度実行し、後でAdobe Commerceにアクセスしてみてください。
