---
title: 「Adobe Commerce 2.4.0 問題：ストアフロントの生メッセージデータの表示」
description: この記事では、ストアフロント上のすべてのエラーメッセージがスペースではなく「+」記号で表示される場合の問題の解決策を説明します。 この解決策は、エラーメッセージを読みやすくするのに役立ちます。
exl-id: f44fe434-a320-4e7e-a876-9575921749f3
feature: Storefront
role: Admin
source-git-commit: a1046621259ea49eab74cd6ba3bba550e0c70283
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Adobe Commerce 2.4.0 の問題：ストアフロントの生メッセージデータの表示

この記事では、ストアフロント上のすべてのエラーメッセージがスペースではなく「+」記号で表示される場合の問題の解決策を説明します。 この解決策は、エラーメッセージを読みやすくするのに役立ちます。

## 影響を受ける製品とバージョン

* クラウドインフラストラクチャー 2.4.0 上のAdobe Commerce
* Adobe Commerce オンプレミス 2.4.0。

## 問題

<u> 再現手順：</u>

1. ストアフロントの **新規アカウントを作成** ページに移動します。
1. 登録済みのメールを使用して新しいアカウントを作成します。 次のメッセージが表示されます。

`There+is+already+an+account+with+this+email+address.+If+you+are+sure+that+it+is+your+email+address,+click+here+to+get+your+password+and+access+your+account.`

## 原因：

この問題は、set\\read cookie に関連する PHP 7.4.2 の問題によって発生します。 [PHP のバグ \#79174 setcookie （）はスペースを\&#39;+\&#39;としてエンコードしますが、$\_COOKIE はスペースをデコードしなくなりました ](https://bugs.php.net/bug.php?id=79174) を参照してください。

## 解決策

この問題を解決するには、PHP 7.4.x の別のバージョンを使用してください。PHP 7.4.2 は、Adobe Commerce 2.4.0 ではサポートされていません。

## サポートナレッジベースの関連するリーディング：

* [Commerce 2.4.0 既知の問題：複数のアドレスのチェックアウトにBraintree支払い方法が表示されない](/help/troubleshooting/payments/magento-2-4-0-braintree-not-in-multiple-addresses-checkout.md)
* [Adobe Commerce 2.4.0 の既知の問題：顧客のアクティビティの更新が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-refresh-on-customer-activities-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：輸出税率が機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-known-issue-export-tax-rates-does-not-work.md)
* [Adobe Commerce 2.4.0 の既知の問題：「買い物かごに選択項目を追加」ボタンが機能しない](/help/troubleshooting/miscellaneous/magento-2-4-0-add-selections-to-my-cart-does-not-work.md)
