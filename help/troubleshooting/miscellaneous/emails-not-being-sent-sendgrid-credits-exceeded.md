---
title: Adobe Commerceで SendGrid クレジットを超えてもメールが送信されない
description: この記事では、Adobe Commerceの SendGrid クレジット制限を超えたことが原因でメールが送信されない場合の解決策を説明します。
exl-id: 43438890-665b-4408-8034-e61de8fbbd8b
feature: Communications, Orders
role: Developer
source-git-commit: e04bb0b37e795cae3380e1110e6db95be12036b0
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Adobe Commerceで SendGrid クレジットを超えてもメールが送信されない

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー上のAdobe Commerce 2.3.0 ～ 2.3.7-p1、2.4.0 ～ 2.4.3

## 問題

SendGrid クレジットとは、送信可能なメールの数を指します。 統合ブランチとステージングブランチから送信できるメールは、1 か月に 12,000 件のみです。 クレジットは月の初めに更新されるため、クレジットが不足した場合は更新を待つ必要があります。

送信者の評判が 95% を超える限り、実稼動環境で送信できるメールの数にハードリミットはありません。 評判は、バウンス/拒否されたメールの数と、DNS ベースのスパムレジストリによってドメインが潜在的なスパムソースとしてフラグ設定されているかどうかによって影響を受けます。 実稼動環境では、1 日に合計 12,000 通のメールが割り当てられますが、その数は、過去 5 日間に送信されたメールの平均数に基づいて拡張できます。

## クレジットが超過したかどうかを確認する方法：

クラウドインフラストラクチャー上のAdobe Commerce Pro プランアーキテクチャ：を確認してください。 `/var/log/mail.log`  – 次のようなメッセージが表示されます。

`May 28 21:13:00 <i-node> postfix/error[21335]: BC7941A2BBF: to=<to@email.com>, relay=none, delay=4642, delays=4642/0.56/0/0.03, dsn=4.0.0, status=deferred (delivery temporarily suspended: SASL authentication failed; server smtp.sendgrid.net[ip address] said: 451 Authentication failed: Maximum credits exceeded).`

## 原因：

送信できるメールの数に制限があります。

## 解決策

* 実稼動環境でこのメッセージが表示された場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) そして、上記のメッセージを提供し、クレジットの増加をリクエストします。
* このメッセージが表示されない場合や、Adobe Commerce on cloud infrastructure スタータープランアーキテクチャを使用している場合は、 [サポートチケットを送信](/help/help-center-guide/help-center/magento-help-center-user-guide.md#submit-ticket) そして次のことに触れます `mail.log` ファイルは、クレジットが超過したことを示すものではありません。

## 関連資料

* [SendGrid](https://devdocs.magento.com/cloud/project/sendgrid.html) 開発者向けドキュメントを参照してください。
