---
title: キャッシュフラッシュでデプロイメントに失敗しました：「cache」名前空間で定義されたコマンドがありません」エラー
description: この記事では、デプロイメントが次のエラーで失敗した場合の問題に対する解決策を提供します**キャッシュ名前空間にコマンドが定義されていません**。
feature: Deploy
role: Developer
exl-id: ee2bddba-36f7-4aae-87a1-5dbeb80e654e
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# キャッシュフラッシュでデプロイメントが失敗しました：「cache」名前空間で定義されたコマンドがありません」エラー

>[!WARNING]
>
>実稼動サイトでこれを行う場合は、まずデータベースをバックアップしてから、これらの手順を実行します。

この記事では、デプロイメントが失敗し、ログのエラーの1つが次のようになる場合の問題の解決策を示します。

```
[YEAR-DAYTIME] ERROR: [127] The command "php ./bin/magento cache:flush --ansi --no-interaction" failed.
        There are no commands defined in the "cache" namespace.
...
      W:     There are no commands defined in the "cache" namespace.
```

## 影響を受ける製品とバージョン

Adobe Commerce on cloud infrastructure 2.4.x

## イシュー

<u>複製する手順</u>:

展開を試みます。

<u>期待される結果</u>:

正常にデプロイされました。

<u>実際の結果</u>:

正常にデプロイできません。 ログに、次のようなメッセージが表示されるデプロイメントエラーが表示されます。*キャッシュ名前空間にコマンドがありません*。

### 原因

**`core_config_data`** テーブルには、データベースに存在しなくなったストア IDまたはweb サイト IDの設定が含まれています。 これは、別のインスタンス/環境からデータベースバックアップをインポートし、関連するストア/web サイトが削除されたにもかかわらず、それらのスコープの設定がデータベースに残っている場合に発生します。

### Solution

1つのweb サイトしか持っていない場合、web サイトの2番目のテストは適用されず、ストアのテストのみが必要です。

この問題を解決するには、これらの設定から残っている無効な行を特定します。

1. サーバーにSSH接続し、次のコマンドを実行します。

   `bin/magento`

1. エラーメッセージは、削除されたサイトからデータベースに残っている行とテーブルを示す場合があります。 例えば、リクエストされたストアが見つからなかったことを示すエラーは次のとおりです。

   ```...
   In StoreRepository.php line 112:
   
   The store that was requested wasn't found. Verify the store and try again.
   ```

1. この[!DNL MySQL] クエリを実行して、ストアが見つからないことを確認します。これは、手順2のエラーメッセージで示されています。

   ```sql
   select distinct scope_id from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. 次の[!DNL MySQL] ステートメントを実行して、無効な行を削除します。

   ```sql
   delete from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. 次のコマンドを再度実行します。

   `bin/magento`

   リクエストされたID Xを持つweb サイトが見つからなかったことを示す次のようなエラーが発生した場合、web サイトとストアの設定が削除されたデータベースに残っています。

   ```
   In WebsiteRepository.php line 110:
   
   The website with id X that was requested wasn't found. Verify the website and try again.
   ```

   この[!DNL MySQL] クエリを実行し、web サイトが見つからないことを確認します：

   ```sql
   select distinct scope_id from core_config_data where scope='stores' and scope_id not in (select store_id from store);
   ```

1. この[!DNL MySQL] ステートメントを実行して、無効な行をweb サイト設定から削除します。

   ```sql
   delete from core_config_data where scope='websites' and scope_id not in (select website_id from store_website);
   ```

解決策が機能することを確認するには、`bin/magento` コマンドをもう一度実行します。 エラーが表示されなくなり、正常にデプロイできるようになりました。

## 関連トピックス

* [Adobe Commerceのデプロイメントのトラブルシューティング](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter)
* [Cloud UIに「ログスニップ」エラーがある場合のデプロイメントログの確認](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-deployment-log-if-the-cloud-ui-shows-log-snipped-error)
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
