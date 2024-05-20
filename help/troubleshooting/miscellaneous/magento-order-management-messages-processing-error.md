---
title: Adobe Commerce処理エラー用のMagento Order Managementシステム（OMS）
description: この記事では、「bin/magento oms」を実行している CLI で「getMode （）」エラーが発生した場合の問題の解決策を説明します。:messages:Adobe CommerceのMagento Order Managementシステム（OMS）の「プロセス」。
exl-id: 83089465-f810-4a3b-bdb6-4720b44f0b49
feature: System
role: Developer
source-git-commit: 21d5bee77c87b93345e9e730642539f1e6b4730a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Adobe Commerce処理エラー用のMagento Order Managementシステム（OMS）

この記事では、を取得した際の問題の解決策を説明します `getMode()` を実行している CLI のエラー `bin/magento oms:messages:process` Adobe CommerceのMagento Order Managementシステム（OMS）で上書きできます。

## 影響を受ける製品とバージョン

このエラーは、MCOM Connector リリース 3.1.1 および 3.2.0 を使用している場合に発生します。これは MCOM Connector 3.3.0 で解決されます。MDC または MOM バージョンに固有のものではありません。

## 問題

CLI で次のコマンドを実行する場合：

`bin/magento oms:messages:process`

次のようなエラーメッセージが CLI に出力されます。

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

## 原因：

Â この問題は、コネクタが処理を試みた場合に発生します `magento.inventory.source_management` メッセージ。 コネクタは、これらのメッセージを以下のように処理しようとします。 `magento.inventory.source_stock_management.update` モード値を必要とするメッセージ。 にはモードがないので `magento.inventory.source_mangement` メッセージが表示されると、エラーが発生します。

## 解決策

この問題を解決するには、CLI で次の SQL 文を実行します。この SQL 文は、内のすべてのレコードを削除します。 `mcom_api_messages` テーブル：

`delete from mcom_api_messages;`

## 関連資料

OMS ドキュメントを参照 [OMS コネクタの設定チュートリアル](https://omsdocs.magento.com/en/integration/connector/setup-tutorial/).
