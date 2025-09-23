---
title: Redis サービスがクラッシュしました。
description: この記事では、Redis を修正する方法を推奨します。
exl-id: 5eb8fb70-0f41-433a-8d3f-c368781a2d1d
feature: Services
role: Developer
source-git-commit: 649e01b29b59bf77e6396acbeb7a83bd9c67e1ef
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Redis サービスがクラッシュしました。

この記事では、Redis を修正する方法を推奨します。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.2.x.、2.3.x
* Adobe Commerce オンプレミス 2.2.x.、2.3x
* Redis のすべてのバージョン

## 問題

Redis のメモリオーバーフローによる Web サイトの速度低下または停止。

## 原因：

メモリオーバーフローは、Redis サービスがクラッシュする原因となる可能性があります。 ピーク時には、Redis サービスは現在割り当てられているメモリよりも多くのメモリを必要とする場合があります。

## 解決策

現在の構成と使用中のメモリを確認するには、CLI で次のコマンドを実行します。 使用中のメモリ、maxmemory、エビクトキー、Redis のアップ時間を日数でチェックします。

```
redis-cli -p REDIS_PORT -h REDIS_HOST info | egrep --color "(role|used_memory_peak|maxmemory|evicted_keys|uptime_in_days)"
```

*REDIS\_PORT* 変数と *REDIS\_HOST* 変数は `app/etc/env.php` から取得できます。

>[!NOTE]
>
>また、次の CLI コマンドを実行して、Redis のホスト アドレスとポート番号を取得することもできます。
>   
```bash
>   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
>   ```


上記のクエリを実行した結果、空きメモリの割合が 40% 未満であることが示された場合は、[Adobe Commerce サポートにチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) し、Redis サーバーの `maxmemory` 設定の増加をリクエストします。 削除されたキーの値が「0」でない場合、または Redis の稼働時間（日数）が 0 である場合（Redis が本日クラッシュしたことを示す）、[Adobe Commerce サポートにチケットを送信 ](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) して、この問題の調査と修正を依頼する必要があります。

## 関連資料

Redis メモリの詳細については、[Redis メモリ最適化 ](https://redis.io/topics/memory-optimization) を参照してください。
