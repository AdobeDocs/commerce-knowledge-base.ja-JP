---
title: '''[!DNL Live Search] 「管理者」の在庫状況設定に関係なく、在庫切れの製品を表示します。'
description: この記事では、検索ポップオーバーが一部の項目を返す際に、製品一覧ページ（PLP）に「選択に一致する製品が見つかりません」というエラーが表示される既知の問題について説明します。
exl-id: 2a351b83-407c-444a-a761-4932b5b88843
feature: Admin Workspace, Categories, Orders, Products, Search
role: Developer
source-git-commit: 958179e0f3efe08e65ea8b0c4c4e1015e3c5bb76
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# [!DNL Live Search] 管理者の在庫状況設定に関係なく、在庫切れの製品を表示します

>[!IMPORTANT]
>
>この問題は、で修正されました [[!DNL Live Search] [2.0.4]](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/release-notes.html). 最新バージョンをインストールするには、を参照してください。 [更新中 [!DNL Live Search]](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/onboard/install.html#update) を参照してください。

この記事では、製品リストページ（PLP）に次の項目が表示される、既知の問題について説明します *選択内容に一致する製品が見つかりません* 検索ポップオーバーが一部の項目を返す際にエラーが発生しました。

## 影響を受ける製品とバージョン

Adobe Commerce（すべてのデプロイメント方法） 2.4.x

## 問題

[!DNL Live Search] は、Adobe Commerce管理での在庫ステータス設定に関係なく検索結果を表示します。 次の場合でも **[!UICONTROL Display Out-of-Stock Products]** はに設定されています。 *不可*&#x200B;に設定すると、商品が表示されます。 その結果、PLP エラーが発生します *選択内容に一致する製品が見つかりません*.

<u>再現手順</u>:

1. カテゴリを作成し、製品を追加します。 （例：Category = _ジーンズ_、Product1 = _ブルージーンズ_、Product2 = _ブラックジーンズ_）
1. カテゴリ内のすべての製品が在庫切れになります。
1. を設定 **[!UICONTROL Display Out-of-Stock Products]** 対象： *不可*.
1. ストアフロントで、と入力します *ジーンズ* を検索フィールドに入力します。
1. クリック **[!UICONTROL View All]** ポップアップで。

<u>期待される結果</u>:

「」が表示されます。 *選択内容に一致する製品が見つかりません* plp にメッセージがあり、検索ポップアップに製品が表示されません。

<u>実際の結果</u>:

「」が表示されます。 *選択内容に一致する製品が見つかりません* plp に関するメッセージ、および両方の製品が検索ポップアップに表示されます。

## 解決策

現在、この問題に対する解決策はありません。 当社の [!DNL Live Search] チームは、間もなく、を設定する設定を提供します [!DNL Live Search] 製品を正しく表示する。

## 関連資料

[インストール [!DNL Live Search]](https://docs.magento.com/user-guide/live-search/install.html) を参照してください。
