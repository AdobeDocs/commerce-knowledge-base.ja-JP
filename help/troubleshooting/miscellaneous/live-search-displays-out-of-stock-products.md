---
title: 「[!DNL Live Search] は、管理者の在庫状況設定に関係なく、在庫切れの製品を表示します」
description: この記事では、検索ポップオーバーが一部の項目を返す際に、製品一覧ページ（PLP）に「選択に一致する製品が見つかりません」というエラーが表示される既知の問題について説明します。
exl-id: 2a351b83-407c-444a-a761-4932b5b88843
feature: Admin Workspace, Categories, Orders, Products, Search
role: Developer
source-git-commit: 2aeb2355b74d1cdfc62b5e7c5aa04fcd0a654733
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# [!DNL Live Search] 管理者の在庫状況設定に関係なく、在庫切れの製品を表示します

>[!IMPORTANT]
>
>この問題は、[[!DNL Live Search] [2.0.4]](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/release-notes.html) で修正されました。 最新バージョンをインストールするには、ユーザーガイドの [ アップデート  [!DNL Live Search]](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#update) を参照してください。

この記事では、製品リストページ（PLP）に「*選択に一致する製品が見つかりません*」エラーが表示され、検索ポップオーバーで一部の項目が返される既知の問題について説明します。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

Adobe Commerce管理 [!DNL Live Search] の在庫ステータス設定に関係なく、検索結果が表示されます。 **[!UICONTROL Display Out-of-Stock Products]** が *No* に設定されている場合でも、商品が表示されます。 これにより、PLP エラー *選択内容に一致する製品が見つかりません* が発生します。

<u> 再現手順 </u>:

1. カテゴリを作成し、製品を追加します。 （例：Category = _ジーンズ_、Product1 = _Blue Jeans_、Product2 = _Black Jeans_）
1. カテゴリ内のすべての製品が在庫切れになります。
1. **[!UICONTROL Display Out-of-Stock Products]** を *いいえ* に設定します。
1. ストアフロントの検索フィールドに「*Jeans* と入力します。
1. ポップアップの「**[!UICONTROL View All]**」をクリックします。

<u> 期待される結果 </u>:

*選択に一致する製品が見つかりません* というメッセージが PLP に表示され、検索ポップアップに製品が表示されません。

<u> 実際の結果 </u>:

*選択に一致する製品が見つかりません* というメッセージが PLP に表示され、両方の製品が検索ポップアップに表示されます。

## 解決策

現在、この問題に対する解決策はありません。 アドビの [!DNL Live Search] チームは、製品を正しく表示するように [!DNL Live Search] を設定する設定を間もなく提供する予定です。

## 関連資料

ユーザーガイドの [ インストール  [!DNL Live Search]](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/live-search/install)。
