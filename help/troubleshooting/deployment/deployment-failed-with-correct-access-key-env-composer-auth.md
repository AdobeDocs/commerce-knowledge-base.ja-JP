---
title: env:COMPOSER_AUTH または auth.json の正しいアクセスキーでのデプロイメントが失敗します
description: この記事では、「https://repo.magento.com/archives/magento/module-customer-balance/magento-module-customer-balance-100.4.0.0.zip ファイルをダウンロードできませんでした（HTTP/1.1 404 が見つかりませんでした）」というエラーでデプロイメントが失敗した場合の問題の解決策を説明します。
feature: Deploy
role: Admin
exl-id: a18f4213-7381-4001-a5a0-3f8db4525469
source-git-commit: 54ef4e95cf0e3f5822ff5e5c566129fab331f784
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# env:COMPOSER_AUTH または auth.json の正しいアクセスキーでのデプロイメントが失敗します

この記事では、次のようなエラーでデプロイメントが失敗した場合の問題の解決策を提供します。 [デプロイメントログ](/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log):

```
W:   [Composer\Downloader\TransportException]
W:   The "https://repo.magento.com/archives/magento/module-customer-balance/magento-module-customer-balance-100.4.0.0.zip" file could not be downloaded (HTTP/1.1 404 Not Found)
```

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー 2.4.x 上のAdobe Commerce

## 問題  

<u>再現手順</u>:

デプロイを試みます。 

<u>期待される結果</u>:

正常にデプロイされました。

<u>実際の結果</u>:

>[!NOTE]
>
>これはエラーの例です。 （デプロイするAdobe Commerceのバージョンに応じて）別のファイルを示すエラーが発生する場合があります。

デプロイに失敗しました。 のようなエラーが表示されます *「https://repo.magento.com/archives/magento/module-customer-balance/magento-module-customer-balance-100.4.0.0.zip」ファイルをダウンロードできませんでした（HTTP/1.1 404 が見つかりません）* が含まれる [デプロイメントログ](/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).


### 原因：

次のいずれかの場所にある指定されたコンポーザーのアクセス キーは、コードにアクセスできない可能性があります：

* が含まれる `env:COMPOSER_AUTH` プロジェクトレベルでの変数
* が含まれる `auth.json file`。この方が `env:COMPOSER_AUTH` 変数。

### 解決策

を更新 `env:COMPOSER_AUTH` プロジェクトレベルの変数で、コードへのアクセス権を持つキーで設定されていることを確認します。

手順については、次を参照してください [変数レベル](/docs/commerce-cloud-service/user-guide/configure/env/variable-levels) （クラウドインフラストラクチャー上のCommerceに関するガイド）を参照してください。

## 関連資料

* [クラウドリポジトリー上のAdobe Commerceにアクセスできませんでした：デプロイ中に「403 Forbidden」または「404 Not Found」エラーが発生する](/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-commerce-cloud-repo-could-not-be-accessed-403-forbidden-or-404-not-found-error-when-deploying.html)
* [展開エラー：ダウンロード中のエラー 7... ポート 443：接続が拒否されました](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/deployment/deployment-error-downloading-connection-refused-adobe-commerce)
