---
title: '概要： [!DNL Quality Patches Tool]  （QPT） v1.1.39'
description: ここでは、 [!DNL Quality Patches Tool]  （QPT） v1.1.39 で使用可能なパッチによって修正された問題について詳しく説明します。
feature: Tools and External Services
role: Admin, Developer
exl-id: 48563701-0fa0-4c88-943e-78b421b806b5
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 概要：[!DNL Quality Patches Tool] （QPT） v1.1.39

このサブセクションでは、[!DNL Quality Patches Tool] （QPT） v1.1.39 で使用可能なパッチによって修正された問題について詳しく説明します。

QPT v1.1.39 には、次のパッチが含まれています。

1. **ACSD-53704**：報酬ポイントの有効期限が切れた後に、報酬ポイントのバランス履歴が誤って計算される問題を修正しました。
1. **ACSD-53583**:*カテゴリ製品* および *製品カテゴリ* インデクサーの部分的な再インデックスパフォーマンスを向上します。
1. **ACSD-54026**：許可されていないユーザーの `updateCompanyRole` GraphQL リクエストに対する誤ったエラーメッセージを修正しました。
1. **ACSD-54106**：トルコ語のアクセント付き文字に対して、カテゴリ製品を名前で並べ替えると誤って表示される問題を修正しました。
1. **ACSD-52219**：ブックマークビューを頻繁に切り替えると、管理グリッドの保存済みフィルターが期待どおりに動作しない問題を修正しました。
1. **ACSD-54342**：有効なデータのない CSV ファイルを読み込む場合に、誤ったエラーメッセージ *データ構造のエラー：値が混在します* を修正しました。
1. **ACSD-54660**:GraphQLのお客様の注文を `sort_field` と `sort_direction` で並べ替える新しい入力属性 *sort* が追加されました。
1. **ACSD-54776**:2 つ目の web サイト、ストア、ストア表示で、オフの *[!UICONTROL Use Default Value]* フィールドとデフォルト以外の製品フィールドの値が保存されない問題を修正しました。
1. **ACSD-53998**：カスタマーアカウントからログアウトした後、**[!UICONTROL Customer Segment]** に基づく **[!UICONTROL Dynamic Block]** が正しく機能しない問題を修正しました。
1. **ACSD-53204**：修正点 *製品を保存できません。`rest/V1/products/<sku>/media` エンドポイントを使用して製品ギャラリーに画像を追加する同時リクエストを行う際に* エラーが発生します。
1. **ACSD-47657**:AWS資格情報のキャッシングメカニズムが追加されました。 資格情報プロバイダーは、Magentoキャッシュを使用して、EC2 設定用にAWSから取得した資格情報をキャッシュするようになりました。

左側のメニューを使用して、特定のパッチページに移動します。
