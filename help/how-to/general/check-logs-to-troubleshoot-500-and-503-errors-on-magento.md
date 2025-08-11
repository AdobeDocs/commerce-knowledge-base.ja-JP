---
title: ログを確認して、Adobe Commerceの 500 および 503 エラーのトラブルシューティングを行います
description: この記事では、「access.log」と関連ログを確認して、トラフィックやサーバーリソースの不足が原因で発生する可能性のある 503 および 500 エラーのトラブルシューティングを行う方法について説明します。 「access.log」と関連ログを確認すると、クラウドインフラストラクチャー上のAdobe Commerceに関連して問題を引き起こしている可能性のある原因に関する情報を得ることができます。
exl-id: 47d7de6b-3e12-4e79-a5c1-c27a9196b99c
feature: Cloud, Logs
source-git-commit: 66ac9de94e9a4a1eccdb5aac1875ecf0a0637e90
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# ログを確認して、Adobe Commerceの 500 および 503 エラーのトラブルシューティングを行います

この記事では、`access.log` と関連ログを確認して、トラフィックまたはサーバーリソースの不足が原因で発生する可能性のある 503 および 500 エラーのトラブルシューティングを行う方法について説明します。 `access.log` と関連ログを確認すると、クラウドインフラストラクチャー上のAdobe Commerceに関連して、何が問題を引き起こしているかに関する情報を得ることができます。

<!--
Bob - not in TOC
-->

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce、すべて [ サポート対象バージョン ](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=ja)。

これらのサーバーエラーのログを表示するには、web サーバーの `access.log` （例：`<ip address>` `<timestamp>` `<request uri>` `<response code>` `<referer url>`）を確認します

関連ログを確認するには：

1. 次のコマンドを CLI で実行します（クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャの場合）。 または、過去の特定の時点（Adobe Commerce on cloud infrastructure スタータープランアーキテクチャの場合）まで、ログのカバレッジの期間が限られ、ログのローテーションは使用できません。`grep -r "\" [50[0-9]" /path/to/access.log` 過去にエラーが発生した場合は、CLI で次のコマンドを実行します（Pro アーキテクチャのみ）。`zgrep "\" 50[0-9]" /path/to/access.log.<rotation ID>.gz`
1. 次に、`exception.log` と `error.log`、または同等の [ ローテーションされたログ ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=ja#log-rotation) （特定のファイルサイズに達すると自動的にローテーションされ圧縮されるログ）で、同じタイムスタンプを確認して、潜在的なエラーを見つけ、そのエラーを引き起こしている可能性のあるものを確認します。 注：`exception.log` をチェックし、`error.log` に CLI で上記のコマンドを実行し、`access.log` を `exception.log` または `error.log` に置き換えます。

## 関連資料

* [2&rbrace;Cloud Infrastructure ガイドのAdobe Commerce](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=ja) ログの表示と管理 *を参照してください。*
* サポートナレッジベースの [503 エラーのトラブルシューティング ](/help/troubleshooting/miscellaneous/troubleshooting-503-errors.md) を参照してください。