---
title: Adobe Commerce処理エラー用のMagento Order Managementシステム（OMS）
description: この記事では、Adobe CommerceのMagento Order Managementシステム（OMS）で「bin/magento oms:messages:process」を実行している CLI で「getMode （）」エラーが発生した場合の問題の解決策を説明します。
exl-id: 83089465-f810-4a3b-bdb6-4720b44f0b49
feature: System
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Adobe Commerce処理エラー用のMagento Order Managementシステム（OMS）

この記事では、Adobe CommerceのMagento Order Managementシステム（OMS）で `bin/magento oms:messages:process` を実行している CLI で `getMode()` エラーが発生した場合の問題に対する解決策を説明します。

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

Â
この問題は、コネクタがメッセージを処理しよう `magento.inventory.source_management` した場合に発生します。 コネクタは、これらのメッセージを、モード値を必要とする `magento.inventory.source_stock_management.update` メッセージであるかのように処理しようとします。 `magento.inventory.source_mangement` のメッセージにはモードがないので、エラーが発生します。

## 解決策

この問題を解決するには、CLI で以下の [!DNL SQL] 文を実行します。この文は、`mcom_api_messages` テーブル内のすべてのレコードを削除します。

`delete from mcom_api_messages;`

## 関連資料

* OMS ドキュメント [OMS コネクタ設定チュートリアル ](https://commerce-docs.github.io/oms-documentation-archive/integration/connector/setup-tutorial/)
* Commerce実装プレイブックの [ データベーステーブルを変更する際のベストプラクティス ](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/development/modifying-core-and-third-party-tables#why-adobe-recommends-avoiding-modifications)
