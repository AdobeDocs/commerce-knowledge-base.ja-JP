---
title: 新しい統合環境にアクセスする際に親環境にリダイレクト
description: この記事では、クラウドインフラストラクチャー上のAdobe Commerceの問題に対するトラブルシューティング手順を説明します。新しく作成した統合環境にアクセスしようとすると、代わりに親環境に移動します。
exl-id: d1d40c8d-d43c-442e-95c9-76f3cdcafb0e
feature: Cache, Integration, Variables
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 新しい統合環境にアクセスする際に親環境にリダイレクト

この記事では、クラウドインフラストラクチャー上のAdobe Commerceの問題に対するトラブルシューティング手順を説明します。新しく作成した統合環境にアクセスしようとすると、代わりに親環境に移動します。

これを修正するには、データベースの base\_url 値を修正し、`UPDATE_URLS` 変数の値が `true` に設定されていることを確認する必要があります。 詳しくは、以下の節を参照してください。

影響を受けるバージョンとエディション：

* クラウドインフラストラクチャー 2.X.X 上のAdobe Commerce

## 問題

<u> 再現手順 </u>:

1. 既存の統合ブランチをクローンします。
1. 新しい環境にアクセスするための URL をクリックします。

<u> 期待される結果 </u>:

新しく作成された環境に移動します。

<u> 実際の結果 </u>:

親ブランチの環境にリダイレクトされます。

## 解決策

この問題を修正するには、カスタム環境データベースで `base_url` の値（secure と unsecure）を修正し、`.magento.env.yaml` ファイルで `UPDATE_URL` 変数を設定する必要があります。

### データベースの base\_url の値を修正する

データベースの変更は、手動で行うことも、バージョン 2.2.0 以降を使用する場合はAdobe Commerce CLI を使用して行うこともできます。

#### DB の値を手動で修正します

1. データベースに接続します。
1. 次のコマンドを実行します。

```sql
UPDATE core_config_data SET value = %your_new_environment_unsecure_url% WHERE path="web/unsecure/base_url"
```

```sql
update core_config_data set value = %your_new_environment_secure_url% where path="web/secure/base_url"
```

#### Adobe Commerce CLI （バージョン 2.2.X で使用可能）を使用してデータベースを修正します。

1. [Adobe Commerce ファイルシステムの所有者としてログインするか、](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/web-server/apache.html?lang=ja) に切り替えます。
1. 次のコマンドを実行します。

```bash
php <your_magento_install_dir>/bin/magento config:set web/unsecure/base_url http://example.com
php <your_magento_install_dir>/bin/magento config:set web/secure/base_url https://example.com
```

### `UPDATE_URLS` 変数を設定します

ローカルコードベースの `.magento.env.yaml` ファイルで、次のように設定します。

```
 stage:
    deploy:
        UPDATE_URLS: true
```

### 設定キャッシュのクリア

変更を適用するには、次のコマンドを実行して、設定キャッシュをクリーンアップします。

```bash
php <your_magento_install_dir>/bin/magento cache:clean config
```

## 開発者向けドキュメントの関連記事：

[ 変数をデプロイ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=ja)
