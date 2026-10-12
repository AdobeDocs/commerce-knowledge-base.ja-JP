---
title: ログを確認して、Adobe Commerceの500および503 エラーをトラブルシューティングする
description: この記事では、「access.log」および関連するログを確認して、トラフィックまたはサーバーリソース不足が原因で発生する可能性のある503および500 エラーをトラブルシューティングする方法について説明します。 「access.log」と関連するログを表示すると、Adobe Commerce on cloud infrastructureに関連する問題の原因となる可能性のある情報を入手できます。
exl-id: 47d7de6b-3e12-4e79-a5c1-c27a9196b99c
feature: Cloud, Logs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%
---
# ログを確認して、Adobe Commerceの500および503 エラーをトラブルシューティングする

この記事では、トラフィックまたはサーバーリソース不足が原因で発生する可能性のある503および500 エラーのトラブルシューティングを行うために、`access.log`および関連ログを確認する方法について説明します。 `access.log`と関連するログを表示すると、Adobe Commerce on cloud infrastructureに関連する問題の原因となる可能性のある情報を入手できます。

<!--
Bob - not in TOC
-->

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャ上のAdobe Commerce、すべての[ サポートされているバージョン ](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html)。

これらのサーバーエラーのログを表示するには、web サーバーの`access.log`を確認します（例：`<ip address>` `<timestamp>` `<request uri>` `<response code>` `<referer url>`）。

関連するログを確認するには：

1. 現在の日にある場合は、CLIで次のコマンドを実行します（Adobe Commerce on cloud infrastructure Pro プランアーキテクチャの場合）。 ログのカバレッジ時間が制限され、ログのローテーションが利用できないため、過去の特定の時点（クラウドインフラストラクチャ上のAdobe Commerce スタータープランアーキテクチャの場合）までログをローテーションできます。`grep -r "\" [50[0-9]" /path/to/access.log`過去にエラーが発生した場合は、CLIで次のコマンドを実行します（Pro アーキテクチャのみ）。`zgrep "\" 50[0-9]" /path/to/access.log.<rotation ID>.gz`
1. 次に、同じタイムスタンプの`exception.log`と`error.log`または同等の[回転ログ ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#log-rotation) （特定のファイルサイズに達したときに自動的に回転および圧縮されるログ）を確認して、潜在的なエラーを見つけ、原因となった可能性のあるエラーを確認します。 注意：`exception.log`と`error.log`を確認するには、CLIで上記のコマンドを実行しますが、`access.log`を`exception.log`または`error.log`に置き換えます。

## 関連トピックス

* *Adobe Commerce on Cloud Infrastructure ガイド*&#x200B;の「[ ログの表示と管理](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)」を参照してください。
* サポートナレッジベースの[503 エラーのトラブルシューティング ](/help/troubleshooting/miscellaneous/troubleshooting-503-errors.md)を参照してください。