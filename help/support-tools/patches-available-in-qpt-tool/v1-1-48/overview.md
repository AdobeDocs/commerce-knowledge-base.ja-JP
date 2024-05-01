---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.48'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.48。
feature: Tools and External Services
role: Admin, Developer
exl-id: 6170c616-312c-4de3-98dc-e2c27c376608
source-git-commit: 42712af2ce4337cd64b8dea555139e4252fb91cf
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.48

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.48。

QPT v1.1.48 には、次のパッチが含まれています。

1. **ACSD-55566**：が発生した問題を修正します *[!UICONTROL mergeCart mutation]* が次の条件で失敗 *内部サーバーエラー* GraphQLのレスポンスでは、移動元と移動先の買い物かごを結合する際に、バンドルされた同じ商品が含まれています。
1. **ACSD-56546**：設定可能な製品およびバンドルされた製品が次のように表示される問題を修正しました *[!UICONTROL Out of Stock]* 次の場合に店先で *[!UICONTROL Display Out of Stock Product]* 設定が無効です。
1. **ACSD-56635**：読み込みを以下で使用すると、読み込まれた顧客が同じメールアドレスで重複する問題を修正しました [!UICONTROL Account Sharing] をに設定 *[!UICONTROL Global]*.
1. **ACSD-56741**：エラーメッセージを修正します *型 null の値の配列オフセットにアクセスしようとしています* 以下の期間に表示される `setup:upgrade` インデックスメカニズムに関連しないカスタム MySQL トリガーがデータベースに含まれている場合および [!DNL MView].
1. **ACSD-57315**：で新しいトランザクションが作成される問題を修正しました [!DNL PayPal Payflow Pro] 毎回 **[!UICONTROL Fetch]** のトランザクションを表示画面でボタンをクリック [!UICONTROL Admin].
1. **ACSD-57337**：特定の web サイトへのアクセス制限を持つ管理者ユーザーが、内のすべての web サイトの会社を表示できる問題を修正しました *[!UICONTROL Companies]* グリッド。
1. **ACSD-57394**:GraphQLで複数の並べ替えフィールドを使用した、誤った商品の並べ替えを修正します。
1. **ACSD-57565**：が発生した問題を修正します *[!UICONTROL Order]* 期間が更新されるまで、ダッシュボードに間違った注文情報が表示される。 ダッシュボードは、最初の読み込み時に正しい順序の統計を表示するようになりました。
1. **ACSD-57854**：製品GraphQL リクエストが、カテゴリ集計で無効なカテゴリを返す問題を修正しました。
1. **ACSD-58008**：終了日が指定されていない場合に、スケジュールされた更新を更新するとステージング項目の以前のバージョンが削除される問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。

