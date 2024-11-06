---
title: 大きな MySQL テーブルの検索
description: '''サイズの大きいテーブルを特定するには、[ データベースに接続 ] （https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/mysql#connect-to-the-database）の記事の説明に従ってデータベースに接続し、次のコマンドを実行します。ここで、''project_id''は Cloud プロジェクト ID です。'''
exl-id: dc5019bc-ab6c-4568-986f-0a294a0f3ac3
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 大きな MySQL テーブルの検索

大きいテーブルを識別するには、[ データベースへの接続 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/mysql#connect-to-the-database) の記事の説明に従ってデータベースに接続し、次のコマンドを実行します。ここで、`project_id` はクラウドプロジェクト ID です。

```sql
SELECT TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS `Size (MB)`
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = "<project_id>"
ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC;
```

テーブルの完全なリストとそのサイズが表示されます。 リストを確認して、サイズが大きいために注意が必要なテーブルを特定できます。

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
