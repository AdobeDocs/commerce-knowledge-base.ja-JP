---
title: Redis サービスがクラッシュしました。
description: この記事では、Redis を修正する方法を推奨します。
exl-id: 5eb8fb70-0f41-433a-8d3f-c368781a2d1d
feature: Services
role: Developer
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '206'
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

この *REDIS\_PORT* および *REDIS\_HOST* 変数は、次の場所から取得できます `app/etc/env.php`.

上記のクエリを実行した結果、空きメモリの割合が 40% 未満と表示された場合、 [Adobe Commerce サポートへのチケットの送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) の増額の請求 `maxmemory` redis サーバーで設定します。 削除されたキーの値が「0」でない場合、または Redis の稼働時間（日数）が 0 に等しい場合（Redis が今日クラッシュしたことを示します）、次の操作も行う必要があります [Adobe Commerce サポートへのチケットの送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) この問題の調査と修正を要求しています。

## 関連資料

Redis メモリの詳細については、を参照してください。 [Redis メモリ最適化](https://redis.io/topics/memory-optimization).
