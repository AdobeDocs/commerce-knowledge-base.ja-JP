---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.1.41'
description: ここでは、 [!DNL Quality Patches Tool]  （QPT） v1.1.41 で使用可能なパッチによって修正された問題について詳しく説明します。
feature: Tools and External Services
role: Admin, Developer
exl-id: 0040fd03-6e53-4e64-b3dc-997e60fabb8c
source-git-commit: f12e25ac5dd607cc614dd99c90c5e104b2cee6a8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 概要：[!DNL Quality Patches Tool] （QPT） v1.1.41

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.1.41 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.1.41 には、次のパッチが含まれています。

1. **ACSD-54376**：商品が既に買い物かごに追加された後に共有カタログから削除された場合に、買い物かごで発生する問題を修正しました。
1. **ACSD-53722**：異なる範囲のスケジュールされたアップデートがアクティブになると、バンドルされた製品オプションの価格が$0 に変更される問題を修正しました。
1. **ACSD-53643**：無効な製品または在庫切れの製品を使用して発注書を送信すると、注文の合計が正しく表示されない問題を修正しました。 このような発注書の *[!UICONTROL Place Order]* ボタンを非表示にすることで修正されます。
1. **ACSD-54067**：モバイルデバイスで製品ビデオが再生されない問題を修正しました。
1. **ACSD-55414**:MariaDB が EAV entity_id を文字列から整数にキャストしようとした際のパフォーマンスを向上しました。
1. **ACSD-51819**：同じ見積 ID で複数の注文を行うことができる問題を修正しました。
1. **ACSD-53118**：製品に空の属性があるときに、クーポンコードを使用して *[!UICONTROL Cart Price Rule]* が適用される問題を修正しました。
1. **ACSD-54324**:GraphQLの requisition_lists リクエストでページネーションの設定が考慮されず、すべての結果が返される問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。
