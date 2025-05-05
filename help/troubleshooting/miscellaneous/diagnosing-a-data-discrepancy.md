---
title: データの相違の診断
description: この記事では、Magento Business Intelligence（MBI）レポートとクエリまたはサードパーティレポートとの間の不一致のトラブルシューティングに関するソリューションを示します。
exl-id: 7d1156cb-9e9b-4426-a0ca-8890b815c245
feature: Commerce Intelligence
role: Developer
source-git-commit: 1fa5ba91a788351c7a7ce8bc0e826f05c5d98de5
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# データの相違の診断

この記事では、Magento Business Intelligence（MBI）レポートとクエリまたはサードパーティレポートとの間の不一致のトラブルシューティングに関するソリューションを示します。

分析の複雑さに応じて、対応する MBI レポートを生成するには、プラットフォームの様々なファセットに関する知識が必要になる場合があります。 このチェックリストと関連リンクは、レポートの背後にあるロジックを理解するのに役立ち、不一致の原因を特定できます。

1. チームの別のメンバーがレポートを作成した場合は、まず、その分析の目的とパラメーターを確認します。
1. クエリ、サードパーティのレポートツール、または数式に基づいて、MBI レポートと比較する必要のあるデータポイントを生成します。
1. Report Builderの指標リンクまたは [ システムの概要 ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/build/reports/ess-manage-data-metrics.html?lang=ja) タブにアクセスして、[ 指標 ](https://support.magento.com/hc/en-us/articles/360016730971-Understand-View-definitions-of-metrics-filters-columns-and-column-references-in-the-System-Summary) 定義を確認します。
   * データテーブル
   * 操作
   * オペランド列（導出される場合はその計算を含む）（システム・サマリーを使用）
   * タイムスタンプ
   * 購読指標の場合：開始日と終了日
   * フィルター（任意の [ フィルターセット ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/build/reports/ess-manage-data-filters.html?lang=ja) に含まれるフィルターを含む）
1. レポート内の他のデータ操作を確認して確認します。
   * 数式を計算
   * [ グループ化 ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/tutorials/using-visual-report-builder.html?lang=ja#groupby)
   * [ 検討 ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/tutorials/using-visual-report-builder.html?lang=ja)
   * [ 時間オプション ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/tutorials/using-visual-report-builder.html?lang=ja)
   * [ コホート分析 ](https://support.magento.com/hc/en-us/articles/360016504632-Create-cohort-analysis) の場合：コホート日
   * [ コホート分析 ](https://support.magento.com/hc/en-us/articles/360016504632-Create-cohort-analysis)：コホートの観点
1. 不一致に最近のデータが含まれる場合は、「接続」ページの **詳細を更新** セクションを参照して、使用可能な最新のデータポイントを確認します。
1. 分析で使用される指標がデータベース内のテーブルに構築され、そのテーブルから行が削除された場合、テーブルの削除行についてテーブルがチェックされていることと、再チェックの頻度およびテーブルの [ レプリケーション方法 ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/best-practices/data/opt-db-analysis.html?lang=ja) について、MBI サポートチームに確認してください。
1. 同様に、行を追加した後に分析で使用されている列を変更できる場合は、これらの列が [ 変更についてチェック ](https://experienceleague.adobe.com/docs/commerce-business-intelligence/mbi/analyze/warehouse-manager/cfg-data-rechecks.html?lang=ja) されていることと、再チェックの頻度をサポートで確認します。

**まだ足を引っ掛かってる？** ご安心ください。当社がお手伝いします。 [ これらの手順 ](/help/troubleshooting/miscellaneous/mbi-data-discrepancies.md) を使用してリクエストを送信します。

## 関連資料

Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
