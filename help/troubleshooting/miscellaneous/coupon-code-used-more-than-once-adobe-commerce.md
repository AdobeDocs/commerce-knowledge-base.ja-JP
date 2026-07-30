---
title: 「シングルユース向けクーポンを複数回利用」、Adobe Commerce
description: この記事では、カート価格ルールのクーポンが正しく機能しない場合の問題に対する解決策を提供します。 加盟店は1回限りのクーポンを設定し、顧客は複数回ご利用いただけます。
exl-id: 9c81de40-65a3-422d-9053-3c894b863a0a
feature: Orders
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 「シングルユース向けクーポンを複数回利用」、Adobe Commerce

この記事では、カート価格ルールのクーポンが正しく機能しない場合の問題に対する解決策を提供します。 加盟店は1回限りのクーポンを設定し、顧客は複数回ご利用いただけます。


## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.3以降

## イシュー

加盟店は1回限りのクーポンを設定し、顧客は複数回ご利用いただけます。

<u>複製する手順</u>:

1. クーポンを作成し、1回使用するようにクーポンを設定します。
1. チェックアウトに進みます。
1. 作成したクーポンを使用します。
1. 再度チェックアウトに進み、同じクーポンを使用します。

<u>期待される結果</u>:

クーポンは1回のみ使用できます。 メッセージが表示されます：*クーポンコード「COUPON_NAME」が無効です*。

<u>実際の結果</u>:

クーポンは複数回使用できます。


## 原因

販売者は`sales.rule.update.coupon.usage`個の消費者を設定して実行していないため、不適切な動作が発生します。

## Solution

`sales.rule.update.coupon.usage` コンシューマーを`app/etc/env.php` ファイルに追加します。

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

詳しい手順については、開発者用ドキュメントの[ メッセージキューの管理/設定](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues#configuration)を参照してください。

## 関連トピックス

開発者ドキュメントの[ メッセージキューの概要](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework)。
