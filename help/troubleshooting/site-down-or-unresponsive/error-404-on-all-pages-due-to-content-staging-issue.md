---
title: コンテンツのステージングに関する問題が原因で、すべてのページでエラー 404 が発生する
description: この記事では、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure の問題を修正します。これらの問題が発生した場合、ストアフロントページまたはCommerce管理者にアクセスすると 404 エラーが発生します。
exl-id: 62d8ba6e-8550-4e1e-8e8d-8f319c92778a
feature: CMS, Catalog Management, Categories, Page Content, Staging
role: Developer
source-git-commit: ce81fc35cc5b7477fc5b3cd5f36a4ff65280e6a0
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# コンテンツのステージングに関する問題が原因で、すべてのページでエラー 404 が発生する

この記事では、Adobe Commerce オンプレミスおよびAdobe Commerce on cloud infrastructure の問題を修正します。これらの問題が発生した場合、ストアフロントページまたはCommerce管理者にアクセスすると 404 エラーが発生します。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.2.x、2.3.x
* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x、2.3.x

## 問題

>[!NOTE]
>
>この記事は、を実行しようとすると 404 エラーが発生する場合には適用されません [ステージング更新をプレビュー](https://docs.magento.com/user-guide/cms/content-staging-scheduled-update.html#preview-the-scheduled-change). その問題が発生した場合は、を開いてください [サポートチケット](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).

ストアフロントページまたは管理者にアクセスすると、を使用してストアコンテンツアセットのスケジュールされた更新を含む操作を実行した後、404 エラー（「Whoops, our bad..」ページ）が発生する [コンテンツのステージング](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html) （を使用してスケジュールされたストアコンテンツアセットの更新） [Magento\_ステージングモジュール](https://developer.adobe.com/commerce/php/module-reference/)）に設定します。 例えば、スケジュールされた更新を含む製品を削除した場合や、スケジュールされた更新の終了日を削除した場合などです。

ストアのコンテンツアセットには、次のものが含まれます。

* 製品
* カテゴリ
* カタログ価格ルール
* 買い物かご価格ルール
* CMS ページ
* CMS ブロック
* ウィジェット

一部のシナリオについては、以下の原因の節で説明します。

## 原因：

この `flag` データベース （DB）のテーブルに、への無効なリンクが含まれています `staging_update` テーブル。

問題はコンテンツのステージングに関連しています。 次に、2 つの具体的な状況を示します。この問題をトリガーとする状況が他にもある可能性があることに注意してください。

**シナリオ 1:** 次のようなストアコンテンツアセットを削除します。

* コンテンツのステージングで更新がスケジュールされています
* 更新には終了日（更新されたアセットが以前のバージョンに戻る有効期限）があります
* 更新の終了日が過去の日付です

同時に、削除されたアセットにスケジュールされた更新の終了日がない場合、問題が発生しない可能性があります。

**シナリオ 2:** スケジュールされている更新の終了日時を削除しています。

### イシューが関連しているかどうかを特定する

発生している問題がこの記事で説明した問題であるかどうかを識別するには、次の DB クエリを実行します。

```sql
   SELECT f.flag_data >'$.current_version' as flag_version, (su.id IS NOT NULL) as update_exists
   -> FROM flag f
   -> LEFT JOIN staging_update su
   -> ON su.id = f.flag_data >'$.current_version'
   -> WHERE flag_code = 'staging';
```

クエリがテーブルを返す場合 `update_exists` 値は「0」で、への無効なリンクです `staging_update` テーブルがデータベースに存在する場合は、で説明されている手順も同様です。 [ソリューション セクション](#solution) が問題の解決に役立ちます。 を使用したクエリ結果の例を次に示します `update_exists` 「0」に等しい値：

![update_exists_0.png](assets/update_exists_0.png)

クエリがテーブルを返す場合 `update_exists` 値が「1」または空の結果である場合、イシューがステージングの更新に関連していないことを意味します。 を使用したクエリ結果の例を次に示します `update_exists` 「1」に等しい値：

![updates_exist_1.png](assets/updates_exist_1.png)

この場合、を参照してください。 [サイト停止のトラブルシューティング](/help/troubleshooting/site-down-or-unresponsive/magento-site-down-troubleshooter.md) アイデアのトラブルシューティング用。

## 解決策

1. 次のクエリを実行して、への無効なリンクを削除します `staging_update` テーブル：

   ```sql
   DELETE FROM flag WHERE flag_code = 'staging';
   ```

1. cron ジョブが実行されるまで待ちます（適切に設定されている場合は最大 5 分実行されます）。または、cron が設定されていない場合は手動で実行します。

無効なリンクを修正した後、問題を直ちに解決する必要があります。 問題が解決しない場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket).
