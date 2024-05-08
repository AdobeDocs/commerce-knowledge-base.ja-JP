---
title: 「Adobe Commerce 2.4.2 B2B：メールテンプレートでメールが更新されない」
description: この記事では、メールテンプレートの一部の情報を更新してもメールで更新されない、既知のAdobe Commerce 2.4.2 B2B の問題について説明します。 この問題は、顧客情報、通貨レート、通貨記号、メールテンプレートの変更などのメールコンテンツに影響を与えます。 現時点では利用可能なソリューションはありませんが、この記事の最後に回避策があります。
exl-id: 31b7086f-a941-4682-aa07-301ac31d543b
feature: B2B, Communications
role: Developer
source-git-commit: 0ad52eceb776b71604c4f467a70c13191bb9a1eb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Adobe Commerce 2.4.2 B2B：メールテンプレートでメールが更新されない

この記事では、メールテンプレートの一部の情報を更新してもメールで更新されない、既知のAdobe Commerce 2.4.2 B2B の問題について説明します。 この問題は、顧客情報、通貨レート、通貨記号、メールテンプレートの変更などのメールコンテンツに影響を与えます。 現時点では利用可能なソリューションはありませんが、この記事の最後に回避策があります。

## 影響を受ける製品とバージョン

* Adobe Commerce オンプレミス 2.4.2
* Adobe Commerce クラウドインフラストラクチャ 2.4.2
* B2B 1.3.1

## 問題

<u>再現手順</u>:

1. 会社管理者が、フロントエンドで PO （発注書）を作成します。
1. 自動承認メールを確認します。 この **顧客名** / **通貨レート** は期待値である必要があります。
1. 通貨記号を変更（**ストア/設定/通貨設定/通貨オプション**）に設定する必要があります。
1. 顧客管理者が管理画面で別の発注を作成します。
1. 自動承認メールを確認します。

<u>期待される結果：</u>

顧客名と通貨記号はメールで変更され、期待どおりに新しい値が設定されます。

<u>実際の結果</u>:

顧客名と通貨記号はメールでは変更されず、以前の値が使用されています。

## 回避策

Cron ジョブまたはコンシューマーを手動で実行して、新しい情報を反映させます。

## 関連資料

* [メッセージキューの管理](https://devdocs.magento.com/guides/v2.4/config-guide/mq/manage-message-queues.html) 開発者向けドキュメントを参照してください。