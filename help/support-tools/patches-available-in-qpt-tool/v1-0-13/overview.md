---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.0.13'
description: ここでは、 [!DNL Quality Patches Tool]  （QPT） v1.0.13 で使用可能なパッチによって修正された問題について詳しく説明します。
exl-id: c25d2926-2137-4a55-abb2-8c0cbff184c9
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# [!DNL Quality Patches Tool] （QPT） v1.0.13 の概要

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.0.13 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.0.13 には、次のパッチが含まれています。

1. **MCP-87**：大規模なプロファイル向けに、カテゴリ製品と在庫のインデクサーのインデクシング時間を改善しました。
1. **MDVA-13203**：完全な再インデックス後に *Integrity constraint violation search_tmp_ table* エラーが表示される問題を修正しました。
1. **MDVA-19391**:`catalog_category_entity_text` テーブルの説明レコードが NULL なため、`analytics_collect_data` がエラーをスローする問題を修正しました。
1. **MDVA-20376**：注文を行った後、ログインしている顧客の `exception.log` で *customerId = 1 の No such entity* エラーの問題を修正。
1. **MDVA-22150**：設定可能な製品が買い物かごにあり、クーポンが適用されている顧客が、その設定可能な製品が管理者で無効になっている場合にログインできない問題を修正しました。
1. **MDVA-23426**:Adobe Commerceから送信される通知メールに、コンテンツが添付ファイルとして追加された空白本文が含まれる問題を修正しました。
1. **MDVA-23764**: ダイナミック ブロックの表示に影響する `JsFooterPlugin.php` のバグを修正しました。
1. **MDVA-30858**:**[!UICONTROL Reports]** > **[!UICONTROL Sales]** > **[!UICONTROL PayPal]** 決済で [!DNL PayPal] 決済レポートが期待どおりに使用できない問題を修正しました。
1. **MDVA-32545**：管理者から注文を作成したときに請求書が自動的に送信されない問題を修正しました。
1. **MDVA-32714**:GraphQLの商品クエリでカスタマーグループ価格が機能しない問題を修正。
1. **MDVA-33106**：再スケジュールされた製品の変更が cron `run` コマンドの実行後に消去される問題を修正。

左側のメニューを使用して、特定のパッチページに移動します。
