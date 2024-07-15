---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.0.8'
description: このサブセクションでは、 [!DNL Quality Patches Tool]  （QPT） v1.0.8 で使用可能なパッチによって修正された問題について詳しく説明します。
exl-id: 6cd3eabe-067f-4e80-b17f-561290499261
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# [!DNL Quality Patches Tool] （QPT） v1.0.8 の概要

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.0.8 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.0.8 には、次のパッチが含まれています。

1. **MDVA-28357**：標準アナライザーを、[!DNL ElasticSearch] インデックスの SKU フィールドでキーワードトークナイザーを使用したカスタムアナライザーに置き換えて、ワイルドカード検索クエリがハイフン（「–」）を含む SKU で機能するようにします。
1. **MDVA-29954**:*新しい会社登録要求* および *会社へのリンクが完了しました* メールが間違ったアドレスから送信される問題を修正しました。
1. **MDVA-30112**：注文の数が *bunch-size* 値を超えた場合、Adobe Commerceが *pending* ステータスの注文を不整合と見なす問題を修正しました。
1. **MDVA-30963**：製品のフィルター結果が、管理者の *すべてのストアビュー* 範囲に指定された値のみを含むように設定され、値がストアビューレベルで上書きされた製品が含まれる問題を修正しました。
1. **MDVA-31150**：請求書が Rest API 呼び出しによって転記され、注文がストアクレジットおよびギフトカードのアカウントによって部分的に支払われた場合に、ストアクレジットおよびギフトカードの残高がGET請求書 Rest API 呼び出しによって返されない問題を修正します。
1. **MDVA-31242**：グリッドに間違った通貨記号が表示される問題 [!UICONTROL Credit Memo] 修正。
1. **MDVA-31295**：部分的な注文が完了し、品目に課税されたときに報酬ポイントが計算されない問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。
