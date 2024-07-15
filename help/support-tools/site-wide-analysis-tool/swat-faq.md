---
title: Adobe Commerce [!DNL Site-Wide Analysis Tool]  レポートの FAQ
description: プロアクティブなセルフサービスツールで、Adobe Commerce インストールのセキュリティと操作性を確保するための詳細なシステムインサイトおよびレコメンデーションが含まれている中央リポジトリである  [!DNL Site-Wide Analysis Tool] について説明します。
exl-id: 7c843d55-9e2c-4b18-8859-0ebad0ae28cf
feature: Best Practices, Saas, Support, Tools and External Services
role: Admin
source-git-commit: 580ad148cd4346868cd9892a1ae9a4d85f73edce
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Adobe Commerce [!DNL Site-Wide Analysis Tool] Report FAQ

>[!IMPORTANT]
>
>2024 年 4 月 23 日（PT）より、Adobe Commerceのオンプレミス環境のお客様の [!DNL Site-Wide Analysis Tool] は廃止されます。

この記事では、クラウドインフラストラクチャー上のAdobe Commerceのお客様向けに、月ごとまたは四半期ごとに自動的に生成される [!DNL Site-Wide Analysis Tool] レポートについて説明します。

>[!NOTE]
>
>クラウドインフラストラクチャー v2.4.1 以降のAdobe Commerceでは、Commerce管理パネルから [!DNL Site-Wide Analysis Tool] を利用できます。 したがって、[!DNL Site-Wide Analysis Tool] レポートは顧客が直接実行できます。 アクセスの詳細については、[[!DNL Site-Wide Analysis Tool]  ガイド ](https://experienceleague.adobe.com/docs/commerce-operations/tools/site-wide-analysis-tool/access.html) を参照してください。

## [!DNL Site-Wide Analysis Tool] とは

[!DNL Site-Wide Analysis Tool] は、エンドツーエンドの「ポイントインタイム」の顧客サイト分析を（顧客のサイトではなく [!DNL Site-Wide Analysis Tool] 環境内で）実行する SaaS アプリケーションです。 全ての [!DNL Site-Wide Analysis Tool] 関連の顧客サイト情報は、3 時間ごと～1 日 1 回の所定のスケジュールで収集されます。 つまり、[!DNL Site-Wide Analysis Tool] は常に顧客サイトのデータを分析して結果を確認しています。

## [!DNL Site-Wide Analysis Tool] レポートとは

[!DNL Site-Wide Analysis Tool] レポートは、Adobe Commerce サポートチケットシステムを通じてPDFのフォームでユーザーに送信できる、セルフサービスのベストプラクティスの推奨事項に関する結果（問題）のリストです。

## [!DNL Site-Wide Analysis Tool] Report には、どのような情報が含まれますか。

[!DNL Site-Wide Analysis Tool] のレポートで提供されるサイト情報には、次のものが含まれます。

* 結果
   * 概要（実装修正の順序の「優先度」を含む）
   * 検索の説明
   * 事前条件（存在する場合）
   * サイトへの影響
   * 根本原因
   * 推奨事項
* 例外ログ
   * 例外情報を記録
   * 最後の発生日
   * 例外が発生した回数

## 自動 [!DNL Site-Wide Analysis Tool] レポートを受け取るのは誰ですか？

現在、[!DNL Site-Wide Analysis Tool] Health インデックスの値が低い（現在設定されているパフォーマンスしきい値以下の）お客様は、サポートチケットシステムを通じて、実稼動環境の毎月の [!DNL Site-Wide Analysis Tool] レポートを受け取ります。

## Automated quarterly [!DNL Site-Wide Analysis Tool] レポートを受け取るのは誰ですか。

すべてのお客様は、[!DNL Site-Wide Analysis Tool] Health Index に関係なく、サポートチケットシステムを通じて、実稼動環境の四半期ごとの [!DNL Site-Wide Analysis Tool] レポートを受け取ります。

## レポートはどのように配信されますか。

[!DNL Site-Wide Analysis Tool] レポートは、Adobe Commerce サポートチケットシステムによって毎月または四半期ごとに自動的に配信されます。 [!DNL Site-Wide Analysis Tool] レポートは、[!DNL Site-Wide Analysis Tool] ダッシュボードから手動で生成して、デスクトップに保存することもできます。 これらの [!DNL Site-Wide Analysis Tool] レポートは、添付ファイルとしてメールで送信できます。

>[!NOTE]
>
>レコメンデーションを適用した後、レポートを手動で生成してもレコメンデーションは更新されません。レコメンデーションが [!DNL Site-Wide Analysis Tool Dashboard] ージから削除されるまでに数日かかる場合があります。
