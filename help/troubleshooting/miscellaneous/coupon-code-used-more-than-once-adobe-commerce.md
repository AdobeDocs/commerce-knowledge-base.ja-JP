---
title: 1 回限りのクーポンが複数回使用されている、Adobe Commerce
description: この記事では、買い物かごの価格ルールクーポンが正しく機能しない問題の解決策を説明します。 マーチャントは 1 回の使用のためにクーポンを設定し、顧客は複数回使用できます。
exl-id: 9c81de40-65a3-422d-9053-3c894b863a0a
feature: Orders
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 1 回限りのクーポンが複数回使用されている、Adobe Commerce

この記事では、買い物かごの価格ルールクーポンが正しく機能しない問題の解決策を説明します。 マーチャントは 1 回の使用のためにクーポンを設定し、顧客は複数回使用できます。


## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.3 以降

## 問題

マーチャントは 1 回の使用のためにクーポンを設定し、顧客は複数回使用できます。

<u> 再現手順 </u>:

1. クーポンを作成し、1 回の使用でクーポンを設定します。
1. チェックアウトに進みます。
1. 作成したばかりのクーポンを使用します。
1. もう一度チェックアウトに進み、同じクーポンを使用します。

<u> 期待される結果 </u>:

クーポンは 1 回のみ使用できます。 *クーポンコード「COUPON_NAME」が無効です* というメッセージが表示されます。

<u> 実際の結果 </u>:

クーポンは複数回使用できます。


## 原因：

マーチャントは、不適切な行動 `sales.rule.update.coupon.usage` 引き起こす消費者の設定と実行を持っていません。

## 解決策

`sales.rule.update.coupon.usage` コンシューマーを `app/etc/env.php` ファイルに追加します。

```php
...
    'cron_consumers_runner' =>
    array [
        'cron_run' => true,
        'max_messages' => 20000,
        'consumers' =>
        array [
            'sales.rule.update.coupon.usage'
        ]
    ],
...
```

詳細な手順については、開発者向けドキュメントの [ メッセージキューの管理/設定 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues#configuration) を参照してください。

## 関連資料

開発者向けドキュメントの [ メッセージキューの概要 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework)。
