---
title: 「シングルユース向けクーポンを複数回利用」、Adobe Commerce
description: この記事では、カート価格ルールのクーポンが正しく機能しない場合の問題に対する解決策を提供します。 加盟店は1回限りのクーポンを設定し、顧客は複数回ご利用いただけます。
exl-id: 9c81de40-65a3-422d-9053-3c894b863a0a
feature: Orders
role: Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 6c96745ec333f45361f77f8116cd9a5684da0aa0
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
