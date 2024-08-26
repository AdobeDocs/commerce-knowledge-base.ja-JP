---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.1.50'
description: ここでは、 [!DNL Quality Patches Tool]  （QPT） v1.1.50 で使用可能なパッチによって修正された問題について詳しく説明します。
feature: Tools and External Services
role: Admin, Developer
source-git-commit: f62cf4284d7bb99a1ab58df676dfff726c34d327
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 概要：[!DNL Quality Patches Tool] （QPT） v1.1.50

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.1.50 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.1.50 には、次のパッチが含まれています。

1. **ACSD-59280**：バージョン 2.4.4-pX のインストール時に、エラー *未定義メソッド ReflectionUnionType::getName （）の呼び出* が発生する問題を修正。
1. **ACSD-45049**：顧客 *[!UICONTROL Is required]* 属性の設定が Admin の Web サイト範囲に応じて正しく機能しない問題を修正しました。
1. **ACSD-46938**：実 `setup:upgrade` 動中に DB トリガーを再作成する際のパフォーマンスの問題を修正しました。
1. **ACSD-48210**：特定のストア表示で *[!UICONTROL website scope]* 属性を更新すると、グローバルスコープの属性値が上書きされる問題を修正しました。
1. **ACSD-54887**:*[!UICONTROL Persistent Shopping Cart]* を有効にしてカスタマーセッションの有効期限が切れた後に、お客様の買い物かごがクリアされる問題を修正しました。
1. **ACSD-58141**:[!UICONTROL L2 Redis cache] が有効になっており、お客様が管理者から更新されている場合に、ログインしている `PHPSESSID` 客様のストアフロント領域でPOSTリクエストに対して CJA が再生成される問題を修正しました。
1. **ACSD-58352**：リクエストヘッダーでデフォルト以外のストア表示が指定されている場合に、デフォルトのストア表示の戻り属性ラベルがGraphQL API を介して返される問題を修正しました。
1. **ACSD-58442**：幅が *768px* のデバイスがモバイルとして扱われ、メニューとヘッダーがデスクトップではなくモバイルビューに読み込まれる問題を修正しました。
1. **ACSD-58790**:[!DNL Chrome] のモバイル表示の製品詳細ページ画像の *ピンチからズーム* 機能を修正しました。
1. **ACSD-59036**：下限と上限の両方が *$0* に等しい製品価格を読み込む際に発生する例外を修正します。
1. **ACSD-59229**：リクエストで [!UICONTROL X-Magento-Vary] の古い値が原因で、顧客グループ関連の情報が間違ったセグメントに保存される問題を修正しました。
1. **ACSD-59378**：読み込み時にストアレベルの URL の書き換えが誤って更新される問題を修正しました。
1. **ACSD-59514**：管理領域内のフォームがロックを解除せずに *[!DNL Page Builder]を 5 秒間レンダリングしてい [!DNL Page Builder] 問題を修正。フォーム* 送信後にブラウザーコンソールに表示されるエラーで、変更を保存できない。
1. **ACSD-60303**:HTMLの縮小が有効になっている場合に、管理者から注文できない問題を修正しました。
1. **ACSD-60441**：バックエンドから生成された統合アクセストークンを使用 `V1/customers REST API` る際に、エンドポイントを介して顧客を更新する問題を修正しました。

左側のメニューを使用して、特定のパッチページに移動します。

