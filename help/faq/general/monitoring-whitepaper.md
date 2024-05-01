---
title: のファクトシートの監視 [!DNL Adobe Commerce on cloud pro infrastructure]
description: このドキュメントでは、Adobe Commerce インフラストラクチャのモニタリングと通知について説明します。
exl-id: 01342d8d-2123-4455-b1a5-a08a5805b046
feature: Cloud
source-git-commit: 4926bcff19b8c4c7e2a9a9dfb0cb1fc72a9821ba
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# のファクトシートの監視 [!DNL Adobe Commerce on cloud pro infrastructure]

このドキュメントでは、Adobe Commerce インフラストラクチャのモニタリングと通知について説明します。

監視により、マーチャント、システムインテグレーター、Adobeの内部チームは、サイトの可用性とディスク容量の不足のトラブルシューティングを行うことができます。

## 問題のトラブルシューティングと解決

Adobe Commerce インスタンスには通常、カスタムコードと設定が含まれています。 Adobeは、カスタムコードおよび設定の問題をサポートも解決もしません。 Adobeは、マーチャントがナレッジベースの問題のトラブルシューティングと特定に役立ち、予防と解決のための推奨ソリューションとベストプラクティスを提供します。 マーチャントおよびパートナーは、以下の表を使用して、監視対象と誰が解決の責任を負うかを理解することをお勧めします。

通知がトリガーされると、Adobe Commerce サポートチームが問題をトリアージします。 トリアージの一環として、エラーログおよびその他のリソースが分析されます。 トリアージに基づいて追加 [!DNL Zendesk] サポートチケットは、（カスタムアップデートの場合は）マーチャントまたはパートナーか、Adobeの内部チームに作成されて、問題を解決します。

## Adobe Commerce：デフォルトの監視

以下のイベントが監視され、Adobe Commerce チームは特定された問題を解決して伝えるために必要な手順を実行します。

## サイトの可用性の監視

| サイトの可用性 | 説明 |
|------------|------------|
| **目標の監視** | サイトの可用性を追跡する |
| **インストルメント対象** | 独身 [!DNL URL] 高に選択されました [!DNL SLA]. |
| **説明** | サイトの可用性は、指標に関して設定されたしきい値に基づいて決定されます。 チェックが 10 分間失敗し、処理中のアクティブなデプロイメントがない場合は、サイト停止の通知がトリガーされます。 |
| **通知の受信者** | マーチャント/パートナーおよびAdobe。 |
| **Adobe別アクション** | 問題がAdobe Commerce インフラストラクチャ上にある場合は、トリアージと修正を担当します。 |
| **商人の行為** | マーチャント/パートナーによって導入された変更またはカスタムコードが原因の場合は、問題を修正する責任があります。 トラブルシューティングについては、次を参照してください。 [サイト停止のトラブルシューティング](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/site-down-or-unresponsive/magento-site-down-troubleshooter.html). |

## ディスク容量の監視

| ディスク容量の監視 | 説明 |
|------------|------------|
| **目標の監視** | ディスク領域の使用状況を追跡します。 |
| **インストルメント対象** | [!DNL MySQL] ディスクおよびメディア ディスク パーティション。 |
| **指標** | 空きディスク領域は、ホスト上で毎分監視されます。 残りの空き容量が 5% または 2 GB の場合に警告が発生します。 残りの空き領域に設定されている重大なしきい値は 2% または 1 GB です。 |
| **説明** | 通知は、ホストの空きディスク容量に関して構成されたしきい値に基づいて送信されます。 関連するマウントに 1 回だけディスク容量が自動的に追加されます（[!DNL MySQL] またはメディア）を使用して、サイトの停止を防ぎ、マーチャントがディスク領域を解放する時間を確保したり、ディスクの使用量が急激に増加する原因となっているコードやログを特定して解決したりします。 |
| **通知の受信者** | マーチャント/パートナーおよびAdobe。 |
| **Adobe別アクション** | サポートチケットを自動的に発行すると、関連するマウントにディスク領域が自動的に追加されます（[!DNL MySQL] またはメディア）を使用して、サイトの停止を防ぎます。 |
| **商人の行為** | 継続的な警告レベルのディスク容量アラートを受け取るには、以下を参照してください。 <ul><li>[[!DNL Managed alerts for Adobe Commerce]: disk warning アラート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce-disk-warning-alert.html)</li><li>[[!DNL Managed alerts for Adobe Commerce]：ディスク障害アラート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce-disk-critical-alert.html) </li></ul> |
