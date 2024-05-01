---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.31'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.31。
exl-id: 0d93619e-0ae6-4dba-9b76-8aeb026c456d
feature: Tools and External Services
role: Admin
source-git-commit: 7718a835e343ae7da9ff79f690503b4ee1d140fc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.31

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.31。

QPT v1.1.31 には、次のパッチが含まれています。

1. **ACSD-50817**:cron ジョブを最適化します `sales_clean_quotes` に複合インデックスを追加してより高速に実行するには、次の手順に従います `store_id` および `updated_at` 引用符表の列。
1. **ACSD-50345**：次の問題を修正しました。 [!DNL Google reCAPTCHA v2] は、支払いに失敗した後にリロードしません。 [!DNL Google reCAPTCHA v3 Invisible] がチェックアウト時に機能せず、注文できない。 [!UICONTROL PlaceOrder] イベントがトリガーされませんでした。
1. **ACSD-49392**：バンドルされた製品の部分払い戻しの後に注文ステータスがクローズに変更される問題を修正します。
1. **ACSD-51036**：同時 REST API 呼び出し中の競合状態によって、の出荷ステータス情報が上書きされる問題を修正しました [!UICONTROL Items Ordered] テーブル。
1. **ACSD-50858**：カード支払いが失敗した後、クーポンが誤って使用済みとマークされる問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。
