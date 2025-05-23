---
title: 「キャッシュフラッシュでデプロイメントに失敗しました：「キャッシュ」名前空間エラーで定義されたコマンドがありません」
description: この記事では、次のエラーでデプロイメントが失敗した場合の問題の解決策を説明します。**キャッシュ名前空間にコマンドが定義されていません**。
feature: Deploy
role: Developer
exl-id: ee2bddba-36f7-4aae-87a1-5dbeb80e654e
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# キャッシュフラッシュのデプロイメントに失敗しました：「キャッシュ」名前空間にコマンドが定義されていません」エラー

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

<u> 再現手順 </u>:

デプロイを試みます。

<u> 期待される結果 </u>:

正常にデプロイされました。

<u> 実際の結果 </u>:

デプロイに失敗しました。 ログには、次のようなメッセージを含んだデプロイメントエラーが表示されます *キャッシュ名前空間にコマンドがありません*。

### 原因：

**`core_config_data`** テーブルには、データベースに存在しなくなったストア ID または web サイト ID の設定が含まれています。 この問題は、別のインスタンスまたは環境からデータベースバックアップをインポートした場合に、関連するストアまたは web サイトが削除されていても、これらのスコープの設定はデータベースに残ります。

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

1. この [!DNL MySQL] クエリを実行して、手順 2 のエラーメッセージで示されるストアが見つからないことを確認します。

   ```sql
   select distinct scope_id from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. 次の [!DNL MySQL] ステートメントを実行して、無効な行を削除します。

   ```sql
   delete from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. もう一度このコマンドを実行します。

   `bin/magento`

   次のようなエラーが表示される場合は、リクエストされた ID X の web サイトが見つからなかったことを示す、残りの設定があります        データベース内の web サイトと、削除されたストア。

   ```
   In WebsiteRepository.php line 110:
   
   The website with id X that was requested wasn't found. Verify the website and try again.
   ```

   次の [!DNL MySQL] クエリを実行し、Web サイトが見つからないことを確認します。

   ```sql
   select distinct scope_id from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. 次の [!DNL MySQL] ステートメントを実行して、Web サイト設定から無効な行を削除します。

   ```sql
   delete from core_config_data where scope='websites' and scope_id not in (select website_id from store_website);
   ```

ソリューションが動作したことを確認するには、`bin/magento` コマンドを再度実行します。 エラーが表示されなくなり、正常にデプロイできます。

## 関連資料

* [Adobe Commerce デプロイメントのトラブルシューティング ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter)
* [Cloud UI に「ログのスニッピング」エラーがあるかどうかをデプロイメントログで確認する ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error)
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
