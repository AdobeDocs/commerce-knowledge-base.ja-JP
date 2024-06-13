---
title: 「'デプロイメントに失敗しました：'キャッシュ'名前空間エラーで定義されたコマンドがありません'」
description: この記事では、次のエラーでデプロイメントが失敗した場合の問題の解決策を説明します。**キャッシュ名前空間にコマンドが定義されていません**。
feature: Deploy
role: Developer
exl-id: ee2bddba-36f7-4aae-87a1-5dbeb80e654e
source-git-commit: 1a8a4e1eada859a6712a43536d7bad26d1ce1244
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# デプロイメントに失敗しました：「キャッシュ」名前空間エラーで定義されたコマンドがありません

>[!WARNING]
>
>実稼動サイトでバックアップを行う場合は、次の手順を実行する前に、まずデータベースをバックアップします。

この記事では、デプロイメントが失敗し、ログ内のエラーのいずれかが次のような場合の問題の解決策を説明します。

```
[YEAR-DAYTIME] ERROR: [127] The command "php ./bin/magento cache:flush --ansi --no-interaction" failed.
        There are no commands defined in the "cache" namespace.
...
      W:     There are no commands defined in the "cache" namespace.
```

## 影響を受ける製品とバージョン

クラウドインフラストラクチャー 2.4.x 上のAdobe Commerce

## 問題  

<u>再現手順</u>:

デプロイを試みます。 

<u>期待される結果</u>:

正常にデプロイされました。

<u>実際の結果</u>:

デプロイに失敗しました。 ログには、次のようなメッセージを含むデプロイメントエラーが表示されます *キャッシュ名前空間にコマンドがありません*.

### 原因：

この **core_config_data** テーブルには、データベースに存在しなくなったストア ID または web サイト ID の設定が含まれています。 この問題は、別のインスタンスまたは環境からデータベースバックアップをインポートした場合に、関連するストアまたは web サイトが削除されていても、これらのスコープの設定はデータベースに残ります。

### 解決策

1 つの web サイトしかない場合、web サイトの 2 番目のテストは適用されず、ストアのテストのみが必要です。

この問題を解決するには、これらの設定に残っている無効な行を特定します。

1. サーバーに SSH で接続し、次のコマンドを実行します。

   `bin/magento`

1. エラーメッセージは、削除されたサイトからデータベースに残っている行とテーブルを示している場合があります。 例えば、次のエラーは、リクエストされたストアが見つからなかったことを示します。

   ```...
   In StoreRepository.php line 112:
   
   The store that was requested wasn't found. Verify the store and try again.
   ```

1. この MySql クエリを実行して、手順 2 のエラーメッセージで示されるストアが見つからないことを確認します。 

   ```sql
   select distinct scope_id from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. 次の MySql ステートメントを実行して、無効な行を削除します。 

   ```sql
   delete from core_config_data where scope='stores' and scope_id not in (select store_id from store); 
   ```

1. もう一度このコマンドを実行します。

   `bin/magento`

   次のような、リクエストされた ID X の web サイトが見つからなかったことを示すエラーが表示された場合は、web サイトと削除されたストアのデータベースに設定が残っています。

   ```
   In WebsiteRepository.php line 110:
   
   The website with id X that was requested wasn't found. Verify the website and try again.
   ```

   次の MySql クエリを実行して、web サイトが見つからないことを確認します。

   ```sql
   select distinct scope_id from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. 次の MySql ステートメントを実行して、web サイト設定から無効な行を削除します。

   ```sql
   delete from core_config_data where scope='websites' and scope_id not in (select website_id from store_website);
   ```

ソリューションが動作したことを確認するには、 `bin/magento` もう一度コマンド。 エラーが表示されなくなり、正常にデプロイできます。

## 関連資料

* [Adobe Commerce導入のトラブルシューティング](/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html)
* [Cloud UI に「ログのスニペット」エラーがあるかどうかをデプロイメントログで確認しています](/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error.html)
