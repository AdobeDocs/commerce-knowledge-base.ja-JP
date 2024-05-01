---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.0.13'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.0.13.
exl-id: c25d2926-2137-4a55-abb2-8c0cbff184c9
feature: Tools and External Services
role: Admin
source-git-commit: 1d2e0c1b4a8e3d79a362500ee3ec7bde84a6ce0d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# [!DNL Quality Patches Tool] （QPT） v1.0.13 の概要

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.0.13.

QPT v1.0.13 には、次のパッチが含まれています。

1. **MCP-87**：大規模なプロファイル向けのカテゴリ製品およびストックインデクサーのインデックス作成時間が改善されました。
1. **MDVA-13203**：が発生した問題を修正します *整合性制約違反 search_tmp_ table* 完全な再インデックス後にエラーが表示される。
1. **MDVA-19391**：の問題を修正します `analytics_collect_data` の説明レコードが NULL なため、がエラーをスローしています `catalog_category_entity_text` テーブル。
1. **MDVA-20376**：の問題を修正しました *customerId = 1 の該当するエンティティがありません* のエラー `exception.log` （受注後のログイン顧客の場合）
1. **MDVA-22150**：設定可能な製品が買い物かごにあり、その設定可能な製品が管理者で無効になっている場合、クーポンが適用されている顧客がログインできない問題を修正しました。
1. **MDVA-23426**:Adobe Commerceから送信される通知メールに、コンテンツが添付ファイルとして追加された空白の本文が含まれる問題を修正しました。
1. **MDVA-23764**：のバグを修正しました `JsFooterPlugin.php` これは、ダイナミック ブロックの表示に影響します。
1. **MDVA-30858**：の問題を修正しました [!DNL PayPal] 以下では決済レポートを使用できません **[!UICONTROL Reports]** > **[!UICONTROL Sales]** > **[!UICONTROL PayPal]** 想定どおりの決済。
1. **MDVA-32545**：管理者から注文を作成した際に請求書が自動的に送信されない問題を修正しました。
1. **MDVA-32714**:GraphQL製品クエリで顧客グループ価格が機能しない問題を修正しました。
1. **MDVA-33106**：再スケジュールされた製品の変更が cron の後で消去される問題を修正します `run` コマンドが実行されます。

左側のメニューを使用して、特定のパッチページに移動します。
