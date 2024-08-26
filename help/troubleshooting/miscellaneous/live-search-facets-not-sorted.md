---
title: 「[!DNL Live Search] ファセットがアルファベット順に並べ替えられていません」
description: この記事では、 [!DNL Live Search]  ファセットがアルファベット順に並べ替えられていない場合のトラブルシューティング情報を提供します。
feature: Admin Workspace, Categories, Search
role: Developer
source-git-commit: 5387edb46281fc536402f8ce0a5e2a77c1bd4193
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL Live Search] ファセットはアルファベット順に並べ替えられていません

## 影響を受ける製品とバージョン

Adobe Commerce バージョン 2.4.x 以降

すべてのAdobe Commerce ストアフロントファセットは、対応する属性に割り当てられた入力タイプに関係なく、単一選択オプションを使用してアルファベット順に並べ替えられます。

ただし、エッジケースによっては、ファセットが [[!DNL Live Search]  ファセットワークスペース ](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/live-search/live-search-admin/facets/faceting-workspace) で設定されているようにアルファベット順に並べ替えられない場合があります。 回避策として、「製品属性」セクションで製 [!UICONTROL Admin] 属性を並べ替えることができます。

1. **[!UICONTROL Admin]** サイドバーで、**ストア**/*属性*/**製品** に移動します。
1. テーブルから属性を選択します。

   ![ 属性リスト ](assets/attribute-list.png)

1. 並べ替える値を持つ属性を開き、**属性情報**/**プロパティ** を選択します。
1. **管理オプション** で、属性値を並べ替えることができます。

   ![ 属性の並べ替え ](assets/sort-attributes.png)
