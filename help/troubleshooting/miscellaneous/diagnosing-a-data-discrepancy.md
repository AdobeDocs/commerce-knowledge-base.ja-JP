---
title: データの相違の診断
description: この記事では、Magento Business Intelligence（MBI）レポートとクエリまたはサードパーティレポートとの間の不一致のトラブルシューティングに関するソリューションを示します。
exl-id: 7d1156cb-9e9b-4426-a0ca-8890b815c245
feature: Commerce Intelligence
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# データの相違の診断

この記事では、Magento Business Intelligence（MBI）レポートとクエリまたはサードパーティレポートとの間の不一致のトラブルシューティングに関するソリューションを示します。

分析の複雑さに応じて、対応する MBI レポートを生成するには、プラットフォームの様々なファセットに関する知識が必要になる場合があります。 このチェックリストと関連リンクは、レポートの背後にあるロジックを理解するのに役立ち、不一致の原因を特定できます。

1. チームの別のメンバーがレポートを作成した場合は、まず、その分析の目的とパラメーターを確認します。
1. クエリ、サードパーティのレポートツール、または数式に基づいて、MBI レポートと比較する必要のあるデータポイントを生成します。
1. をレビューして確認します [指標](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/build/reports/ess-manage-data-metrics.html) 定義（Report Builderの指標リンクから、または [システムの概要](https://support.magento.com/hc/en-us/articles/360016730971-Understand-View-definitions-of-metrics-filters-columns-and-column-references-in-the-System-Summary) タブ：
   * データテーブル
   * 操作
   * オペランド列（導出される場合はその計算を含む）（システム・サマリーを使用）
   * タイムスタンプ
   * 購読指標の場合：開始日と終了日
   * フィルター（すべてに含まれるフィルターを含む） [フィルターセット](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/build/reports/ess-manage-data-filters.html) 適用日時
1. レポート内の他のデータ操作を確認して確認します。
   * 数式を計算
   * [グループ化](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/tutorials/using-visual-report-builder.html#groupby)
   * [視点](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/tutorials/using-visual-report-builder.html)
   * [時間オプション](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/tutorials/using-visual-report-builder.html)
   * の場合 [コホート分析](https://support.magento.com/hc/en-us/articles/360016504632-Create-cohort-analysis): コホート日
   * の場合 [コホート分析](https://support.magento.com/hc/en-us/articles/360016504632-Create-cohort-analysis): コホートの観点
1. 不一致に最近のデータが含まれる場合は、を参照して、利用可能な最新のデータポイントを確認します。 **詳細を更新** 「接続」ページの「」セクション
1. 分析で使用される指標がデータベース内のテーブルに作成され、そのテーブルから行が削除された場合、そのテーブルの削除行がチェックされていることと、再チェックの頻度および [複製方法](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/best-practices/data/opt-db-analysis.html) テーブル用。
1. 同様に、行を追加した後に分析で使用されている列を変更できる場合は、サポートを受けてこれらの列が存在することを確認します [変更をチェックしました](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/analyze/warehouse-manager/cfg-data-rechecks.html)、および再チェックの頻度。

**まだ切り詰められてるの？** ご安心ください。サポートが必要です。 次を使用してリクエストを送信 [これらの説明](/help/troubleshooting/miscellaneous/mbi-data-discrepancies.md).
