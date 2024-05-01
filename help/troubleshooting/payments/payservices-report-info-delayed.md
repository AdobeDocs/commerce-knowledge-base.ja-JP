---
title: 遅延支払サービスレポートデータ
description: この記事では、支払いサービスのレポートデータが遅延する可能性がある理由を説明します。
exl-id: 2f3249d1-be12-45bc-aa73-bef9766509ae
feature: Orders, Payments
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 遅延支払サービスレポートデータ

この記事では、支払いサービスのレポートデータが遅延する可能性がある理由を説明します。

## 影響を受ける製品とバージョン

* [支払いサービス](https://marketplace.magento.com/magento-payment-services.html) は、Adobe Commerce バージョン 2.4.0～2.4.4 と互換性を持つようになりました。

## 問題

支払いサービスのレポートデータ（支払いおよび注文の支払いステータスレポートの場合）は、すぐに同期されない場合があります。

注文に対して請求（キャプチャ）を行った後、または注文に関するクレジット・メモを発行した後は、注文のステータスがすぐに利用できなくなる場合があります。

<u>再現手順</u>:

前提条件：支払いサービス機能を使用して注文が行われます。

1. 注文は [請求済](https://docs.magento.com/user-guide/sales/invoice-create.html) （または [キャンセル済み](https://docs.magento.com/user-guide/sales/order-update.html#cancel-a-pending-order) または [クレジットメモによる払戻](https://docs.magento.com/user-guide/sales/credit-memos.html)） [Admin](https://docs.magento.com/user-guide/stores/admin.html).
1. 注文支払ステータスレポートに移動して、その注文に関する情報を表示します。
1. ステータスの表示内容 `AUTHORIZED`（請求またはその他の注文アクションの前の注文ステータス）。

   Commerceはデータを同期して支払いサービスに送信していないので、新しい注文ステータスはまだレポートで認識されません。

>[!NOTE]
>
>これは、一般的なユースケースの 1 つにすぎません。 以下のような場合に、他の使用例が考えられます。 [注文アクション](https://docs.magento.com/user-guide/sales/order-actions.html) が発生し、該当するレポートでデータがすぐに使用できなくなる。

<u>期待される結果</u>：レポートデータは、注文に対するアクションの直後に入力されます。

<u>実際の結果</u>：完了したばかりの注文アクションの場合、表示されるレポートデータに遅延が生じる場合があります。 支払いレポートには、24～48 時間の遅延が発生する場合があります。 注文支払いステータスレポートには、数時間の遅延が発生する場合があります。

## 原因：

管理画面に表示されるデータのこの遅延に影響する要因は 2 つあります。

* を介してCommerceからデータを同期（エクスポートおよび永続化）する頻度 [管理者の設定](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/configure-admin.html).
* PayPal がレポートデータを公開する期間。

## 解決策

注文支払いステータスレポートの場合：

1. に移動します。 **売上** > **支払いサービス**.
1. クリック **注文支払いステータス** 注文支払ステータスレポート テーブルを表示します。
1. をクリックして再同期を強制する **再同期を強制** 「レポート」 テーブルの右上隅にあるアイコン。
1. 最後に更新されたタイムスタンプの変更と新しいトランザクションがレポートテーブルに読み込まれているのが確認できます。

PayPal の支払いレポートの場合、PayPal のデータ公開期間に依存しているため、予想結果は 24～48 時間の遅延となります。
