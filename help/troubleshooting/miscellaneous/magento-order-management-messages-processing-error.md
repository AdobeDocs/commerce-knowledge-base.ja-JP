---
title: Magento Order Management System （OMS）におけるAdobe Commerceの処理エラー
description: この記事では、Adobe Commerce用Magento Order Management System （OMS）で「bin/magento oms:messages:process」を実行しているCLIで「getMode （）」エラーが発生した場合の問題の解決策を紹介します。
exl-id: 83089465-f810-4a3b-bdb6-4720b44f0b49
feature: System
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%
---
# Magento Order Management System （OMS）におけるAdobe Commerceの処理エラー

この記事では、Adobe Commerce用Magento Order Management System （OMS）で`bin/magento oms:messages:process`を実行しているCLIで`getMode()` エラーが発生した場合の問題の解決策を紹介します。

## 影響を受ける製品とバージョン

このエラーは、MCOM Connector リリース 3.1.1および3.2.0を使用している場合に発生します。 これはMCOM コネクタ 3.3.0で解決されます。 MDCまたはMOMのバージョンに固有ではありません。

## イシュー

CLIで次のコマンドを実行する場合：

`bin/magento oms:messages:process`

次のようなエラーメッセージがCLIに出力されます。

```
<project-id>@<project-id>:~$ php bin/magento oms:messages:process

Processing messages...

PHP Fatal error:Uncaught Error: Call to a member function getMode()
on null in /app/<project-id>/vendor/magento/module-inventory-message-bus/Handler/OnAggregateStockUpdatedSubscriber.php:64

Stack trace:

  #0 [internal function]: Magento\InventoryMessageBus\Handler\OnAggregateStockUpdatedSubscriber->onUpdated(Object(Magento\InventoryMessageBus\Model\Event\OnAggregateStockUpdated))

  #1 /app/<project-id>/vendor/magento/module-service-bus/Message/SingleMessageProcessor.php(81):
  call_user_func(Array, Object(Magento\InventoryMessageBus\Model\Event\OnAggregateStockUpdated))

  #2 [internal function]: Magento\ServiceBus\Message\SingleMessageProcessor->Magento\ServiceBus\Message\\{closure}(Array)

  #3 /app/<project-id>/vendor/magento/module-service-bus/Message/SingleMessageProcessor.php(86):
  array_map(Object(Closure), Array)

  #4 /app/<project-id>/vendor/magento/module-service-bus/Message/Processor.php(110):
  Magento\ServiceBus\Message\SingleMessageProcessor->process(Object(Magento\CommonMessageBus\Message\Message))

  #5 /app/t in /app/<project-id>/vendor/magento/module-inventory-message-bus/Handler/OnAggregateStockUpdatedSubscriber.php
  on line 64
```

## 原因

′
これは、コネクタが`magento.inventory.source_management`個のメッセージを処理しようとしたときに発生します。 コネクタは、これらのメッセージがモード値を必要としない`magento.inventory.source_stock_management.update` メッセージであるかのように処理しようとします。 `magento.inventory.source_mangement` メッセージにモードがないため、エラーが発生します。

## Solution

この問題を解決するには、CLIで次の[!DNL SQL] ステートメントを実行し、`mcom_api_messages` テーブルのすべてのレコードを削除します。

`delete from mcom_api_messages;`

## 関連トピックス

* OMS ドキュメント [OMS コネクタ設定チュートリアル ](https://commerce-docs.github.io/oms-documentation-archive/integration/connector/setup-tutorial/)
* [Commerce実装プレイブックのデータベーステーブルを修正するためのベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
