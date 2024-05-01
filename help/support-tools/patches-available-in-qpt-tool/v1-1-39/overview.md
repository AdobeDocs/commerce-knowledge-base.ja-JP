---
title: '概要： [!DNL Quality Patches Tool] （QPT） v1.1.39'
description: このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.39。
feature: Tools and External Services
role: Admin, Developer
exl-id: 48563701-0fa0-4c88-943e-78b421b806b5
source-git-commit: dccb8dde1666fa0c72c7c94cd94c82daddaadc54
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 概要： [!DNL Quality Patches Tool] （QPT） v1.1.39

このサブセクションでは、で使用可能なパッチによって修正された問題について詳しく説明します。 [!DNL Quality Patches Tool] （QPT） v1.1.39。

QPT v1.1.39 には、次のパッチが含まれています。

1. **ACSD-53704**：報酬ポイントの有効期限が切れた後に、報酬ポイントのバランス履歴が誤って計算される問題を修正します。
1. **ACSD-53583**：の部分再インデックスのパフォーマンスを向上します *カテゴリ製品* および *製品カテゴリ* インデクサー。
1. **ACSD-54026**：の誤ったエラーメッセージを修正します `updateCompanyRole` 許可されていないユーザーに対するGraphQL リクエスト。
1. **ACSD-54106**：トルコ語のアクセント付き文字に対して、カテゴリ製品を名前で並べ替えると誤って表示される問題を修正しました。
1. **ACSD-52219**：ブックマークビューを頻繁に切り替えると、管理グリッドの保存済みフィルターが期待どおりに動作しない問題を修正しました。
1. **ACSD-54342**：誤ったエラーメッセージを修正します *データ構造のエラー：値が混在しています* 有効なデータのない CSV ファイルを読み込む場合。
1. **ACSD-54660**：新しい入力属性が追加されました *並べ替え* GraphQLで顧客の注文を並べ替えるには `sort_field` および `sort_direction`.
1. **ACSD-54776**：チェックされていない問題を修正します *[!UICONTROL Use Default Value]* また、デフォルト以外の製品フィールドの値は、2 番目の web サイト、ストア、ストアの表示では保存されません。
1. **ACSD-53998**：が発生する問題を修正します **[!UICONTROL Dynamic Block]** に基づく **[!UICONTROL Customer Segment]** は、カスタマーアカウントからログアウトした後、正しく機能しません。
1. **ACSD-53204**：修正点 *商品を保存できません。* を使用して製品ギャラリーに画像を追加する同時リクエストを行う際にエラーが発生する `rest/V1/products/<sku>/media` エンドポイント。
1. **ACSD-47657**:AWS資格情報のキャッシングメカニズムを追加しました。 資格情報プロバイダーは、Magentoキャッシュを使用して、EC2 設定用にAWSから取得した資格情報をキャッシュするようになりました。

左側のメニューを使用して、特定のパッチページに移動します。
