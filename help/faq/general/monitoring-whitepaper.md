---
title: 監視ファクト・シート  [!DNL Adobe Commerce on cloud pro infrastructure]
description: このドキュメントでは、Adobe Commerce インフラストラクチャのモニタリングと通知について説明します。
exl-id: 01342d8d-2123-4455-b1a5-a08a5805b046
feature: Cloud
source-git-commit: 27fed162416c619a08d757279a3405f1fa72e976
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# [!DNL Adobe Commerce on cloud pro infrastructure] の監視ファクト シート

このドキュメントでは、Adobe Commerce インフラストラクチャのモニタリングと通知について説明します。

監視を使用すると、マーチャント、システムインテグレーター、Adobeの内部チームは、サイトの可用性とディスク容量の不足のトラブルシューティングを行うことができます。

## 問題のトラブルシューティングと解決

Adobe Commerce インスタンスには通常、カスタムコードと設定が含まれています。 Adobeは、カスタムコードおよび設定に関する問題をサポートまたは解決しません。 Adobeは、マーチャントがナレッジベースの問題のトラブルシューティングと特定を行うのを支援し、予防と解決に関する推奨ソリューションとベストプラクティスを提供します。 マーチャントおよびパートナーは、以下の表を使用して、監視対象と誰が解決の責任を負うかを理解することをお勧めします。

通知がトリガーされると、Adobe Commerce サポートチームが問題をトリアージします。 トリアージの一環として、エラーログおよびその他のリソースが分析されます。 トリアージに基づいて、（カスタムアップデートの場合は）マーチャントまたはパートナー、またはAdobeの内部チームに対して、問題を解決するための追加の [!DNL Zendesk] サポートチケットが作成されます。

## Adobe Commerce：デフォルトの監視

以下のイベントが監視され、Adobe Commerce チームは特定された問題を解決して伝えるために必要な手順を実行します。

## サイトの可用性の監視

| サイトの可用性 | 説明 |
|------------|------------|
| **目標の監視** | サイトの可用性を追跡する |
| **インストルメンテーション対象** | 高 [!DNL SLA] 用に単一の [!DNL URL] が選択されました。 |
| **説明** | サイトの可用性は、指標に関して設定されたしきい値に基づいて決定されます。 チェックが 10 分間失敗し、処理中のアクティブなデプロイメントがない場合は、サイト停止の通知がトリガーされます。 |
| **通知の受信者** | マーチャント/パートナーおよびAdobe |
| **Adobeの対応** | 問題がAdobe Commerce インフラストラクチャ上にある場合は、トリアージと修正を担当します。 |
| **商人の訴え** | マーチャント/パートナーによって導入された変更またはカスタムコードが原因の場合は、問題を修正する責任があります。 トラブルシューティングについては、「[ サイトダウンのトラブルシューティング ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/site-down-or-unresponsive/magento-site-down-troubleshooter.html)」を参照してください。 |

## ディスク容量の監視

| ディスク容量の監視 | 説明 |
|------------|------------|
| **目標の監視** | ディスク領域の使用状況を追跡します。 |
| **インストルメンテーション対象** | [!DNL MySQL] ディスクとメディア ディスクのパーティション。 |
| **指標** | 空きディスク領域は、ホスト上で毎分監視されます。 残りの空き容量が 5% または 2 GB の場合に警告が発生します。 残りの空き領域に設定されている重大なしきい値は 2% または 1 GB です。 |
| **説明** | 通知は、ホストの空きディスク容量に関して構成されたしきい値に基づいて送信されます。 関連するマウント（[!DNL MySQL] またはメディア）に 1 回だけディスク領域が自動的に追加され、サイトの停止を防ぐとともに、ディスク領域をクリアしたり、ディスク使用量の急激な増加を引き起こしているコードやログを特定して解決したりする時間をマーチャントに与えます。 |
| **通知の受信者** | マーチャント/パートナーおよびAdobe |
| **Adobeの対応** | サポートチケットを自動的に発行すると、関連するマウント（[!DNL MySQL] またはメディア）にディスク領域が自動的に追加され、サイトの停止が回避されます。 |
| **商人の訴え** | 継続的な警告レベルのディスク容量アラートを受け取るには、以下を参照してください。 <ul><li>[[!DNL Managed alerts for Adobe Commerce]: disk warning アラート ](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-disk-warning-alert)</li><li>[[!DNL Managed alerts for Adobe Commerce]: disk critical アラート ](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce-disk-critical-alert) </li></ul> |
