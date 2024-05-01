---
title: 大きな MySQL テーブルの検索
description: '''サイズの大きいテーブルを特定するには、[ データベースに接続 ] （https://devdocs.magento.com/cloud/project/project-conf-files_services-mysql.html#connect-to-the-database）の記事の説明に従ってデータベースに接続し、次のコマンドを実行します。ここで、''project_id''は Cloud プロジェクト ID です。'''
exl-id: dc5019bc-ab6c-4568-986f-0a294a0f3ac3
source-git-commit: c1c2bd29e14f4cbfffb235801e95ec7cbb7c7a55
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 大きな MySQL テーブルの検索

大きいテーブルを識別するには、の説明に従って、データベースに接続します [データベースへの接続](https://devdocs.magento.com/cloud/project/project-conf-files_services-mysql.html#connect-to-the-database) を作成し、次のコマンドを実行します。このコマンドの条件は次のとおりです。 `project_id` はクラウドプロジェクト ID :

```sql
SELECT TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS `Size (MB)`
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = "<project_id>"
ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC;
```

テーブルの完全なリストとそのサイズが表示されます。 リストを確認して、サイズが大きいために注意が必要なテーブルを特定できます。
