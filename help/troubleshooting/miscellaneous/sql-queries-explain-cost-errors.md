---
title: 「SQL クエリ：コストエラーの説明」
description: この記事では、失敗した SQL クエリを実行した際の EXPLAIN コストエラーの解決策を説明します。 PostgreSQL は、[EXPLAIN コマンド ] （https://www.postgresql.org/docs/9.5/static/using-explain.html）と呼ばれるものを使用して、SQL クエリのコストを決定します。 また、このコマンドを使用するように SQLReport Builderを構築しました。つまり、コストが高すぎると見なされる場合（クエリの実行に必要なリソース量がしきい値を超える場合）、クエリは実行されず、EXPLAIN メッセージが表示されます。
exl-id: 6f6df66a-665e-46a8-ad4c-842a0270c4eb
feature: Commerce Intelligence
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# SQL クエリ：コストエラーの説明

この記事では、失敗した SQL クエリを実行した際の EXPLAIN コストエラーの解決策を説明します。 PostgreSQL は EXPLAIN コマンド [ と呼ばれるものを使用して SQL 問い合わせのコストを決定します ](https://www.postgresql.org/docs/9.5/static/using-explain.html) また、このコマンドを使用するように SQLReport Builderを構築しました。つまり、コストが高すぎると見なされる場合（クエリの実行に必要なリソース量がしきい値を超える場合）、クエリは実行されず、EXPLAIN メッセージが表示されます。

これが発生する理由はいくつかあります。 受信するメッセージ、その意味およびトラブルシューティング方法を次に示します。

## クエリを実行できません。 EXPLAIN のコスト値\[xxx\] は、このクエリを実行するには高すぎます。

このメッセージが表示された場合は、クエリの実行にコストがかかりすぎていると見なされたことを意味します。 この状況に対しては、2 つの推奨事項があります。1 つは、コストのかかる操作であるため、クエリから ORDER BY 句を排除することです。 2 つ目は、[ 最適化の記事 ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/best-practices/data/optimizing-your-sql-queries.html?lang=ja) のヒントに従って、クエリを調整することです。

## クエリを実行できません。 このクエリは、10,000 の制限を超える\[xxx\] 行を返します

この場合、可能な結果の数は、SQL Report Builderに設定された最大数を超えています。 結果の数を減らす方法はいくつかあります。

* クエリにフィルターを追加してみてください。
* 可能な場合は、LIMIT を使用します。 一部のテーブルには多数の行があり、結果を制限することで行の制限を回避できます。

## EXPLAIN 応答を解析できません。

エラー。 このメッセージは通常、おそらく私たちの側で問題が発生したことを意味します。 このエラーが引き続き表示される場合は、サポートにお問い合わせください。
