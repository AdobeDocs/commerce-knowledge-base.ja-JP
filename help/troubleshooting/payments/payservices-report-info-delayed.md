---
title: 遅延支払サービスレポートデータ
description: この記事では、支払いサービスのレポートデータが遅延する可能性がある理由を説明します。
exl-id: 2f3249d1-be12-45bc-aa73-bef9766509ae
feature: Orders, Payments
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 遅延支払サービスレポートデータ

この記事では、支払いサービスのレポートデータが遅延する可能性がある理由を説明します。

## 影響を受ける製品とバージョン

* [ 支払いサービス ](https://marketplace.magento.com/magento-payment-services.html) は、Adobe Commerce バージョン 2.4.0 から 2.4.4 と互換性を持つようになりました。

## 問題

支払いサービスのレポートデータ（支払いおよび注文の支払いステータスレポートの場合）は、すぐに同期されない場合があります。

注文に対して請求（キャプチャ）を行った後、または注文に関するクレジット・メモを発行した後は、注文のステータスがすぐに利用できなくなる場合があります。

<u> 再現手順 </u>:

前提条件：支払いサービス機能を使用して注文が行われます。

1. 注文は、[ 管理者 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) で [ 請求 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order) （またはキャンセル [ または ](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/admin/admin) クレジットメモによる払い戻し [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos) されます。
1. 注文支払ステータスレポートに移動して、その注文に関する情報を表示します。
1. ステータスは `AUTHORIZED` と表示されます。これは、請求またはその他の注文アクションの前の注文ステータスです。

   Commerceはデータを同期して支払いサービスに送信していないので、新しい注文ステータスはまだレポートで認識されません。

>[!NOTE]
>
>これは、一般的なユースケースの 1 つにすぎません。 [ 注文アクション ](https://experienceleague.adobe.com/ja/docs/commerce-admin/stores-sales/order-management/orders/orders#actions) が発生し、該当するレポートですぐにデータを使用できない場合は、他のユースケースが考えられます。

<u> 期待される結果 </u>:
レポートデータは、注文に対するアクションが発生した直後に入力されます。

<u> 実際の結果 </u>:
完了したばかりの注文アクションの場合、表示されるレポートデータに遅延が生じる場合があります。 支払いレポートには、24～48 時間の遅延が発生する場合があります。 注文支払いステータスレポートには、数時間の遅延が発生する場合があります。

## 原因：

管理画面に表示されるデータのこの遅延に影響する要因は 2 つあります。

* [ 管理者の設定 ](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/configure-admin.html?lang=ja) を使用して、Commerceからデータを同期（書き出しと保持）する頻度。
* PayPal がレポートデータを公開する期間。

## 解決策

注文支払いステータスレポートの場合：

1. **営業**/**支払いサービス** に移動します。
1. **注文支払ステータス** をクリックして、注文支払ステータスレポートテーブルを表示します。
1. 再同期を強制するには、「レポート」テーブルの右上隅にある **再同期を強制** アイコンをクリックします。
1. 最後に更新されたタイムスタンプの変更と新しいトランザクションがレポートテーブルに読み込まれているのが確認できます。

PayPal の支払いレポートの場合、PayPal のデータ公開期間に依存しているため、予想結果は 24～48 時間の遅延となります。
